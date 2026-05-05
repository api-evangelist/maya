---
title: "Automation API：旧エンジン削除と 2027 エンジン"
url: "https://blog.autodesk.io/automation-api-old-engine-removal-and-add-2027-engines/"
date: "Wed, 22 Apr 2026 00:09:00 +0000"
author: "Toshiaki Isezaki"
feed_url: "https://blog.autodesk.io/feed/"
---
<figure class="wp-block-image"><img alt="A timeline diagram depicting the lifecycle policies of various Autodesk Design Automation API core engine versions, highlighting registration and execution statuses of AppBundle and Activity." class="wp-image-42724" height="1080" src="https://i0.wp.com/blog.autodesk.io/wp-content/uploads/2025/01/da_lifecycle.jpg?resize=1024%2C576&amp;ssl=1" width="1920" /></figure>



<p class="wp-block-paragraph"><a href="https://blog.autodesk.io/design-automation-api-core-engine-lifecycle-policy/" rel="noreferrer noopener" target="_blank"><strong>Design Automation API：コアエンジンライフサイクルポリシー</strong></a> でご案内していますとおり、<strong><a href="https://aps.autodesk.com/en/docs/design-automation/v3/developers_guide/engine-lifecycle/" rel="noreferrer noopener" target="_blank">Engine Lifecycle Policy</a></strong>&nbsp;に従って、公開から6年を経過した 2021 バージョンに対応する古いコアエンジン バージョンが、2026年3月29日に廃止されています。</p>



<p class="wp-block-paragraph">削除対象となったコアエンジンバージョンは、次のとおりです。</p>



<ul class="wp-block-list">
<li><strong>Autodesk.3dsMax.2021</strong></li>



<li><strong>Autodesk.AutoCAD.24</strong></li>



<li><strong>Autodesk.Inventor.2021</strong></li>



<li><strong>Autodesk.Revit.2021</strong></li>
</ul>



<p class="wp-block-paragraph">製品更新のタイミングが他のデスクトップ製品と異なる Autodesk Fusion に合わせて、次の Fusion Automation API コア バージョンが2026年2月24日に削除されています。</p>



<ul class="wp-block-list">
<li><strong>Autodesk.Fusion+2605_00</strong></li>
</ul>



<p class="wp-block-paragraph">同様に、次のコアエンジンバージョンが2026年5月5日に削除される予定です。</p>



<ul class="wp-block-list">
<li><strong>Autodesk.Fusion+2606_00</strong></li>
</ul>



<p class="wp-block-paragraph">また、次のコアエンジンバージョンは2026年6月29日に削除される予定です。</p>



<ul class="wp-block-list">
<li><strong>Autodesk.Fusion+2701_00</strong></li>
</ul>



<p class="wp-block-paragraph">同エンジン バージョンをお使いの場合には、事前に新しいバージョンに移行していただくようお願いいたします。</p>



<p class="wp-block-paragraph">また、2027 バージョンのデスクトップ製品のリリースにともない、対応するエンジン バージョンが利用可能になっています。新しいエンジン バージョンと <a href="https://aps.autodesk.com/en/docs/design-automation/v3/reference/http/engines-id-GET/">GET engines/:id</a> エンドポイントが返すレスポンス ボディは次のとおりです。</p>



<ul class="wp-block-list">
<li><strong>Autodesk.AutoCAD+26_0</strong></li>
</ul>


<div class="wp-block-code has-background has-small-font-size">
	<div class="cm-editor">
		<div class="cm-scroller">
			
<pre><code><div class="cm-line">{</div><div class="cm-line">    &quot;productVersion&quot;: &quot;26.0&quot;,</div><div class="cm-line">    &quot;deprecationDate&quot;: &quot;2030-03-29&quot;,</div><div class="cm-line">    &quot;description&quot;: &quot;AutoCAD 2027 (Xenon) Core Engine&quot;,</div><div class="cm-line">    &quot;version&quot;: 45,</div><div class="cm-line">    &quot;id&quot;: &quot;Autodesk.AutoCAD+26_0&quot;</div><div class="cm-line">}</div></code></pre>
		</div>
	</div>
</div>


<ul class="wp-block-list">
<li><strong>Autodesk.Revit+2027</strong></li>
</ul>


<div class="wp-block-code has-background has-small-font-size">
	<div class="cm-editor">
		<div class="cm-scroller">
			
<pre><code><div class="cm-line">{</div><div class="cm-line">    &quot;productVersion&quot;: &quot;27.0&quot;,</div><div class="cm-line">    &quot;deprecationDate&quot;: &quot;2030-03-29&quot;,</div><div class="cm-line">    &quot;description&quot;: &quot;Revit 2027 (RVTDA 03-19-2026).&quot;,</div><div class="cm-line">    &quot;version&quot;: 132,</div><div class="cm-line">    &quot;id&quot;: &quot;Autodesk.Revit+2027&quot;</div><div class="cm-line">}</div></code></pre>
		</div>
	</div>
</div>


<ul class="wp-block-list">
<li><strong>Autodesk.Inventor+2027</strong></li>
</ul>


<div class="wp-block-code has-background has-small-font-size">
	<div class="cm-editor">
		<div class="cm-scroller">
			
<pre><code><div class="cm-line">{</div><div class="cm-line">    &quot;productVersion&quot;: &quot;31.00&quot;,</div><div class="cm-line">    &quot;deprecationDate&quot;: &quot;2030-03-29&quot;,</div><div class="cm-line">    &quot;description&quot;: &quot;Inventor 2027&quot;,</div><div class="cm-line">    &quot;version&quot;: 49,</div><div class="cm-line">    &quot;id&quot;: &quot;Autodesk.Inventor+2027&quot;</div><div class="cm-line">}</div></code></pre>
		</div>
	</div>
</div>


<ul class="wp-block-list is-style-checkmark-list">
<li>2027 バージョン相当の 3ds Max Automation API コアエンジン バージョンは、公開が少し遅れています。</li>
</ul>



<p class="wp-block-paragraph">利用可能な Automation API コアエンジン バージョンの取得方法は、<strong><a href="https://blog.autodesk.io/design-automation-api-obtaining-supported-engines/">Autodesk Developer Blog : Design Automation API: サポート エンジン一覧の取得</a> </strong>の記事でご案内しています。</p>
