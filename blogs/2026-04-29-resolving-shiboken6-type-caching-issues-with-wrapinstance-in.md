---
title: "Resolving Shiboken6 type caching issues with wrapInstance in Maya 2027"
url: "https://blog.autodesk.io/resolving-shiboken6-type-caching-issues-with-wrapinstance-in-maya-2027/"
date: "Wed, 29 Apr 2026 02:49:50 +0000"
author: "Cheng Xi Li"
feed_url: "https://blog.autodesk.io/feed/"
---
<div class="wp-block-jetpack-markdown"><h3>The Problem</h3>
<p>A customer recently ran into a behavior change in PySide6/Shiboken6 between Maya 2026 and Maya 2027. Their workflow involves retrieving the correct Python type from a raw pointer by first wrapping it as a QObject and inspecting its metaObject:</p>
<pre><code class="language-Python">qObj = shiboken6.wrapInstance(int(ptr), QtCore.QObject)
metaObj = qObj.metaObject()
cls = metaObj.className()
superCls = metaObj.superClass().className()
...
return shiboken6.wrapInstance((int)ptr, classType)
</code></pre>
<p>In Maya 2026 and earlier, they could get correct type from the second wrapInstance. But in Maya 2027, they could only get QObject instead.</p>
<h3>Root Cause</h3>
<p>It is caused by a new feature which has been introduced since <a href="https://doc.qt.io/qtforpython-6/release_notes/shiboken6_release_notes.html#id16">Qt 6.7</a>.</p>
<blockquote>
<p><a href="https://qt-project.atlassian.net/browse//PYSIDE-31">PYSIDE-31</a> Shiboken.wrapInstance() now returns existing instances (preserving ids).</p>
</blockquote>
<p>Back in <a href="https://code.qt.io/cgit/pyside/pyside-setup.git/tree/sources/shiboken6/shibokenmodule/typesystem_shiboken.xml?h=6.5.3#n19">Qt 6.5.3</a>(Maya 2026), the wrapInstance will always return a new instance:</p>
<pre><code class="language-C++"> auto *pyType = reinterpret_cast&amp;lt;PyTypeObject *&amp;gt;(%2); 
            if (Shiboken::ObjectType::checkType(pyType)) { 
                %PYARG_0 = Shiboken::Object::newObject(pyType, 
                                                       reinterpret_cast&amp;lt;void *&amp;gt;(%1), 
                                                       false, true); 
            } else { 
                PyErr_SetString(PyExc_TypeError, &quot;You need a shiboken-based type.&quot;); 
            }
</code></pre>
<p>But in <a href="https://code.qt.io/cgit/pyside/pyside-setup.git/tree/sources/shiboken6/shibokenmodule/shibokenmodule.cpp?h=6.8.3#n10">Qt 6.8.3</a>(Maya 2027), it became below:</p>
<pre><code class="language-C++">auto *pyType = reinterpret_cast&lt;PyTypeObject *&gt;(%2); 
if (Shiboken::ObjectType::checkType(pyType)) { 
    auto *ptr = reinterpret_cast&lt;void *&gt;(%1); 
    if (auto *wrapper = Shiboken::BindingManager::instance().retrieveWrapper(ptr)) { 
        Py_INCREF(wrapper); 
        %PYARG_0 = reinterpret_cast&lt;PyObject *&gt;(wrapper); 
    } else { 
        %PYARG_0 = Shiboken::Object::newObject(pyType, ptr, false, true); 
    } 
} else { 
    PyErr_SetString(PyExc_TypeError, &quot;You need a shiboken-based type.&quot;); 
}
</code></pre>
<h3>Workaround</h3>
<p>There isn’t a documented way to remove wrapped object from the BindingManager. However, if you check <a href="https://code.qt.io/cgit/pyside/pyside-setup.git/tree/sources/shiboken6/shibokenmodule/typesystem_shiboken.xml?h=6.8.3#n14">typesystem_shiboken.xml</a>, there is an undocumented method(invalidate):</p>
<pre><code class="language-xml">&lt;add-function signature=&quot;invalidate(PyObject*)&quot;&gt; 
        &lt;inject-code&gt; 
            Shiboken::Object::invalidate(%1); 
        &lt;/inject-code&gt; 
&lt;/add-function&gt; 
</code></pre>
<p>The method code be tracked to <a href="https://code.qt.io/cgit/pyside/pyside-setup.git/tree/sources/shiboken6/libshiboken/basewrapper.cpp?h=6.8.3#n1312">libshiboken/basewrapper.cpp</a>. And it will call <a href="https://code.qt.io/cgit/pyside/pyside-setup.git/tree/sources/shiboken6/libshiboken/basewrapper.cpp?h=6.8.3#n1331">recursive_invalidate</a> which calls <a href="https://code.qt.io/cgit/pyside/pyside-setup.git/tree/sources/shiboken6/libshiboken/bindingmanager.cpp?h=6.8.3#n287">BindingManager::releaseWrapper</a>.</p>
<p>By calling it before the second wrapInstance, I could get a new wrapped instance with correct type.</p>
<p>Since it is an undocumented method, please use it with caution.</p>
</div>
