<h2 id="root"><code>:root</code></h2>
<p>CSS에서 문서의 최상위 요소를 나타낸다.
브라우저에서는 <code>&lt;html&gt;</code> 태그를 의미한다.</p>
<h3 id="목적">목적</h3>
<p>주로 CSS 변수를 선언하는 데 사용된다.
전역 스타일 적용에도 사용할 수 있으나, 일반적으로 변수 선언에 많이 쓰인다.</p>
<h3 id="예시">예시</h3>
<pre><code class="language-css">:root {
  --primary-color: #3498db;
  --font-size: 16px;
}

body {
  color: var(--primary-color);
  font-size: var(--font-size);
}</code></pre>
<h2 id="-universal-selector">* (Universal Selector)</h2>
<p>모든 요소를 삭 선택한다.</p>
<h3 id="목적-1">목적</h3>
<p>문서 내 모든 요소에 스타일을 적용할 때 사용된다.
브라우저의 기본 스타일 초기화나 기본 스타일 설정에 많이 쓰인다.
너무 많은 요소에 복잡한 스타일을 적용할 경우 주의가 필요하다.</p>
<h3 id="예시-1">예시</h3>
<pre><code class="language-css">* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}</code></pre>
<h2 id="root-vs-"><code>:root</code> vs <code>*</code></h2>
<table>
<thead>
<tr>
<th><strong>특징</strong></th>
<th><strong><code>:root</code></strong></th>
<th><strong><code>*</code></strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>적용 범위</strong></td>
<td>문서 최상위 요소 (<code>&lt;html&gt;</code>)</td>
<td>문서 내 모든 요소</td>
</tr>
<tr>
<td><strong>주요 사용 목적</strong></td>
<td>CSS 변수 선언, 전역 스타일 관리</td>
<td>초기화, 기본 스타일 설정</td>
</tr>
<tr>
<td><strong>사용 사례</strong></td>
<td>변수 선언: <code>--primary-color</code>, 전역 접근</td>
<td>Reset CSS, 기본 마진/패딩 제거</td>
</tr>
<tr>
<td><strong>성능 고려</strong></td>
<td>제한적 적용</td>
<td>모든 요소에 적용하므로 성능에 영향 가능</td>
</tr>
</tbody></table>
<blockquote>
<p>목적에 따라 올바르게 사용하여 유지보수성과 성능을 모두 챙겨보자!</p>
</blockquote>