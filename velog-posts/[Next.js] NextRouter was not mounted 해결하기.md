<h2 id="💥error">💥Error</h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/5fc17636-f6ef-4c91-b6e9-912694a0cba8/image.png" /></p>
<h2 id="🪄solution">🪄Solution</h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/000a8df9-f25f-4809-b569-2c6f53c23905/image.png" /></p>
<p>나의 경우 두 번째 상황에 해당되므로,
<code>useRouter</code>를 <code>&quot;next/router&quot;</code>가 아닌 <code>&quot;next/navigation&quot;</code> 모듈에서 불러오도록 수정하여 해결했다.</p>
<h2 id="👓summary">👓Summary</h2>
<ol>
<li>next13 이상의 버전을 사용하고 있고</li>
<li><code>app</code> directory 안에서</li>
<li><code>&quot;use client&quot;</code>와 <code>useRouter</code>를 함께 사용하려면</li>
<li><code>useRouter</code>를 <code>&quot;next/navigation&quot;</code> 모듈에서 불러와야 한다.</li>
</ol>
<h2 id="💡reference">💡Reference</h2>
<p><a href="https://nextjs.org/docs/messages/next-router-not-mounted">nextjs.org/docs</a></p>