<h2 id="코드">코드</h2>
<p>첨에 선이 안뵈길래 inline이라 그런가 싶어 block 넣어봤다가 너비를 지정하지 않아서 생기는 문제란 걸 알았다!
웁스</p>
<pre><code class="language-js">const textWithLineStyle = css`
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 22px;
  width: 100%; /* textWithLine이 차지할 너비 설정. 중요! */
  gap: 15px; /* 선과 텍스트 사이 간격 */

  &amp;::before,
  &amp;::after {
    content: &quot;&quot;;
    flex-grow: 1;
    height: 1px;
    background-color: #d6d6d6;
  }
`;</code></pre>
<p><code>emotion</code>의 <code>css prop</code> 방식이다.</p>
<h2 id="적용">적용</h2>
<p>요런 넉김</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/40658548-44ab-48c2-9874-8b338e3bc8a5/image.png" /></p>