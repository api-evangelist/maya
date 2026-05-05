---
title: "Why your AutoCAD OEM installer silently crashes on customer machines (and how to fix it)"
url: "https://blog.autodesk.io/why-your-autocad-oem-installer-silently-crashes-on-customer-machines-and-how-to-fix-it/"
date: "Sat, 18 Apr 2026 12:25:55 +0000"
author: "Madhukar Moogala"
feed_url: "https://blog.autodesk.io/feed/"
---
<p>We just closed a support ticket that took a month of back-and-forth, and it ended up being a really interesting lesson in how antivirus software works under the hood.</p>

    <p>If you build products on AutoCAD OEM, you might have run into this scenario: a customer runs your installer, the UI flashes for a split second, and then it just quits. Sometimes you might get a generic error dialog, but often, it&#8217;s just a completely silent crash. You test it locally and it works perfectly. It&#8217;s incredibly frustrating to debug.</p>

    <h3>The log that made no sense</h3>
    <p>Since AutoCAD OEM uses the Autodesk ODIS installation framework, we had the customer send over their <code>DDA.log</code>. When we looked through it, we found a contradiction that made us scratch our heads.</p>
    
    <p>The log showed the installer successfully verifying the digital signature of <code>DownloadManager.exe</code>. This means the file was successfully extracted and was physically sitting on the customer&#8217;s hard drive. But literally the next line in the log showed the Windows <code>CreateProcess</code> call failing to launch it, throwing an <strong>Error Code 2 (File Not Found)</strong>.</p>

    <p>How does Windows fail to find a file it just verified a millisecond ago?</p>

    <h3>The Antivirus Hijack</h3>
    <p>It turns out, this is how antivirus programs (like Windows Defender, Norton, or Avast) quietly hijack processes. They use a Windows Registry feature called <strong>Image File Execution Options (IFEO)</strong>.</p>

    <p>Microsoft originally built IFEO so developers could attach debuggers to their applications. But AV vendors realized they could use it to block malware. Because the ODIS installer downloads payloads and silently extracts executables in the background, aggressive AV heuristics sometimes freak out and flag it as a dropper.</p>

    <p>To block the &#8220;threat&#8221;, the AV creates an IFEO registry key for the installer&#8217;s executables and adds a <code>Debugger</code> string value pointing to &#8220;Blocked&#8221; or a dummy file. From that moment on, whenever Windows tries to launch <code>DownloadManager.exe</code>, it intercepts the call and tries to run the non-existent debugger instead. When that fails, Windows throws the &#8220;File Not Found&#8221; error back to our installer, causing it to crash.</p>

    <p>The most annoying part is that even if the customer completely uninstalls their antivirus to troubleshoot, these registry keys are often left behind. The OS remains permanently rigged to block your installer.</p>

    <h3>A quick way to check</h3>
    <p>If you want to quickly scan a customer&#8217;s machine to see if any executables are being hijacked by IFEO, you can run this PowerShell script. It searches the registry and spits out any keys that have a Debugger attached:</p>

    <pre><code class="language-powershell">Get-ChildItem "Registry::HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options" -Recurse -ErrorAction SilentlyContinue |
    ForEach-Object {
        $p = Get-ItemProperty -Path $_.PSPath -ErrorAction SilentlyContinue
        if ($p.Debugger -or $p.GlobalFlag -or $p.VerifierDlls) {
            [PSCustomObject]@{
                Key          = $_.PSChildName
                Debugger     = $p.Debugger
                GlobalFlag   = $p.GlobalFlag
                VerifierDlls = $p.VerifierDlls
                Path         = $_.PSPath
            }
        }
    }</code></pre>

    <h3>How to fix it</h3>
    <p>Once we figured out what was happening, the fix was actually really simple. You just need to clear out the leftover debugger blocks in the registry.</p>

    <ol>
        <li>Open the Windows Registry Editor (<code>regedit</code>).</li>
        <li>Navigate to: <code>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options</code></li>
        <li>Look for any sub-keys matching Autodesk or ODIS executables (like <code>DownloadManager.exe</code>, <code>ProcessManager.exe</code>, <code>AdskAccessUIHost.exe</code>, or <code>Setup.exe</code>).</li>
        <li>If you see a <code>Debugger</code> value inside any of those folders, delete it.</li>
    </ol>

    <p>Our partner had the customer clear those blocked registry keys, and the installations immediately went through without a hitch. Hopefully, this saves someone else a month of troubleshooting!</p>



<p class="wp-block-paragraph"></p>
