<h2 id="복습">복습</h2>
<p>Hydration은 서버에서 렌더링된 정적인 HTML 콘텐츠를 클라이언트 측에서 JavaScript와 React 상태로 활성화하여 동적이고 인터랙티브한 웹 페이지로 만드는 과정을 말한다.</p>
<p>예를 들어 서버에서 생성된 HTML이 아래와 같을 때,</p>
<pre><code class="language-html">&lt;div id=&quot;root&quot;&gt;
  &lt;button&gt;Click me&lt;/button&gt;
&lt;/div&gt;</code></pre>
<p>클라이언트에서 React가 이 HTML에 연결하여 이벤트를 활성화하는 과정을 거쳐</p>
<pre><code class="language-javascript">const App = () =&gt; {
  const handleClick = () =&gt; alert(&quot;Clicked!&quot;);
  return &lt;button onClick={handleClick}&gt;Click me!&lt;/button&gt;;
};

hydrateRoot(document.getElementById(&quot;root&quot;), &lt;App /&gt;);</code></pre>
<p>코드 속 우리가 의도한 button이 사용자에게 보여지게 된다.</p>
<p>저번에 헷갈렸던 부분은 hydration은 React의 기능인데
왜 next의 장점이라고 하는것인지. 였는데 SSR에서만 hydration이 필요하겠구나 싶었다. CSR 환경에서는 클라이언트가 HTML을 동적으로 생성하기 때문이다.</p>
<p>정리해보면,</p>
<ul>
<li>CSR 환경에서는 서버에서 미리 생성된 HTML이 없고 React가 처음부터 클라이언트에서 모든 것을 렌더링하기 때문에 Hydration이 필요없다.</li>
<li>Hydration은 React꺼고,
Next.js는 이를 기반으로 SSR과 CSR을 결합하여 활용하는 프레임워크다.</li>
</ul>
<h2 id="거런데">거런데</h2>
<p>SSR은 모든 컴포넌트에 발생하지만,
client에서 hydrate되는 컴포넌트는 <code>use client</code> 지시어를 가지고 있는 컴포넌트들 뿐이다. 헉슨</p>
<p>놀라기 전에 곰곰히 다시 생각해보면 use client 지시어가 없는 컴포넌트는 hydration의 도움이 필요가 없다는 걸 알 수 있다.</p>
<p>use client의 의미는
저기 거짝. 이 컴포넌트 말이지 클라이언트에서 인터랙티브 해야 해
와 같다.</p>
<p>hydration의 역할은 <strong>컴포넌트를 React client와 연결해서 동적이고 인터랙티브하게 만들어주는 것</strong>이라서, <code>use client</code> 지시어가 필요없는 컴포넌트는 hydration도 필요가 없는거다.</p>
<p>이렇게 <code>use client</code> 지시어가 없는 컴포넌트를 서버 컴포넌트라고 부른다.
클라이언트 컴포넌트는 backend에서 render -&gt; frontend에서 hydrate 되고
서버 컴포넌트는 backend에서 render -&gt; 끝이다.</p>
<p>사용자는 클라이언트 컴포넌트의 자스 코드만 다운로드 받으면 되는 것이고,
이것은 페이지 로딩 속도를 빠르게 만든다.</p>
<h2 id="reference">Reference</h2>
<p>니꼬쌤</p>