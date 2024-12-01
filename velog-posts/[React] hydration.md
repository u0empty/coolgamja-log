<h1 id="hydration">hydration</h1>
<p><code>hydration</code>은 React에서 서버 사이드 렌더링(SSR)된 HTML을 클라이언트에서 동적으로 활성화하는 과정이다.
즉, 서버에서 한 번 렌더링된 정적 HTML이, hydration을 거치며 interactive한 페이지로 바뀌는 것이다.
이 과정은 SSR에서만 발생하는데, CSR 환경에는 React가 처음부터 클라이언트에서 모든 것을 렌더링하기 때문에 hydration을 거칠 필요가 없다.</p>
<h2 id="좀-더-자세히">좀 더 자세히</h2>
<p>React에서는 CSR과 SSR을 결합하여 더 효율적인 페이지 로딩을 구현한다.
SSR을 통해 서버에서 HTML을 렌더링하여 클라이언트로 전달하면 사용자는 처음에 정적 HTML을 보게 된다.
그 때 클라이언트 측에서 정적 HTML을 React 컴포넌트로 <strong>전환</strong>함으로써 상태 업데이트나 이벤트 처리가 가능하게 만든다.
여기서 이러한 <strong>전환</strong>을 처리하는 과정이 <code>hydration</code>이다.</p>
<h2 id="hydration-과정">hydration 과정</h2>
<ol>
<li><p>서버 사이드 렌더링 (SSR)
서버는 React 컴포넌트를 렌더링하여 완성된 HTML을 클라이언트에게 보낸다.
이때 서버에서 렌더링된 HTML은 정적이고 동적이지 않은 상태이다.
SSR된 HTML이 브라우저에서 먼저 표시된다.</p>
</li>
<li><p>hydration
클라이언트가 서버에서 받은 HTML을 로드한 후, React는 이 HTML을 카만 두고 클라이언트에서 JavaScript를 실행하여 해당 HTML을 동적으로 활성화한다.
React는 서버에서 보낸 HTML과 클라이언트 측의 React 애플리케이션 상태를 일치시켜 렌더링된 DOM을 동적으로 관리한다.</p>
</li>
</ol>
<h2 id="예를-들어">예를 들어</h2>
<p>서버에서 생성된 HTML이 아래와 같을 때,</p>
<pre><code class="language-html">&lt;div id=&quot;root&quot;&gt;
  &lt;button&gt;Click me!&lt;/button&gt;
&lt;/div&gt;</code></pre>
<p>클라이언트에서 React가 이 HTML에 연결하여 이벤트를 활성화하는 과정을 거쳐</p>
<pre><code class="language-js">const App = () =&gt; {
  const handleClick = () =&gt; alert(&quot;Clicked!&quot;);
  return &lt;button onClick={handleClick}&gt;Click me!&lt;/button&gt;;
};

hydrateRoot(document.getElementById(&quot;root&quot;), &lt;App /&gt;);</code></pre>
<p>코드 속 우리가 의도한 button이 사용자에게 보여지게 된다.</p>
<h2 id="hydartion-메서드">hydartion 메서드</h2>
<h3 id="reactdomhydrate">ReactDOM.hydrate()</h3>
<p><code>ReactDOM.hydrate()</code>는 서버에서 전달된 HTML을 기반으로 React 애플리케이션을 클라이언트 측에서 동적으로 활성화하는 메서드이다.
서버에서 보낸 HTML은 정적이므로, React는 이 HTML을 받아서 동적으로 업데이트 가능한 상태로 만들기 위해 <code>hydrate()</code> 메서드를 사용한다.</p>
<pre><code class="language-js">ReactDOM.hydrate(&lt;App /&gt;, document.getElementById(&quot;root&quot;));</code></pre>
<p>거런데 이 메서드는 React 18 이전까지 주로 사용되던 방법이다.</p>
<h3 id="hydrateroot">hydrateRoot()</h3>
<p>React 18부터 새로 도입된 <code>hydrateRoot</code>는 더 세밀한 동적 렌더링을 가능하게 하고,
Concurrent Mode와 호환되며, React의 createRoot와 결합되어 더 나은 성능과 안정성을 제공한다.</p>
<pre><code class="language-js">import { hydrateRoot } from &quot;react-dom/client&quot;;

hydrateRoot(document.getElementById(&quot;root&quot;), &lt;App /&gt;);</code></pre>
<p>참고로 React 18부터 도입된
<code>Concurrent Mode</code>는 기존 동기적이었던 React 렌더링 방식을 비동기적으로 만드는 새로운 기능이고,
<code>createRoot</code>는 ReactDOM.render() 메서드의 상위 버전으로 Concurrent Mode와 자동 배치를 지원한다고 한다.</p>
<h2 id="hydration-vs-csr">hydration vs CSR</h2>
<h3 id="csr">CSR</h3>
<p>페이지가 처음 로드될 때, 서버에서 HTML을 전송하는 대신, 빈 HTML 페이지만 전송하고 클라이언트 측에서 JavaScript가 실행되어 페이지를 렌더링한다.
때문에 페이지가 완전히 로드되기까지 시간이 걸리며, 초기 페이지 표시 속도가 느려질 수 있다.</p>
<h3 id="ssr--hydration">SSR + Hydration</h3>
<p>빈 HTML이 아닌 서버에서 렌더링된 HTML을 페이지에 빠르게 표시한다.
고 다음, hydration을 통해 서버로부터 받은 정적 HTML을 동적으로 활성화하므로 페이지 로딩 속도가 빠르고,
&lt;br서버에서 렌더링된 HTML을 검색 엔진이 크롤링할 수 있기에 SEO에도 유리하다.</p>
<h2 id="주의할-점">주의할 점</h2>
<p>hydration이 지연되면 자바스크립트가 로드되고 실행될 때까지 초기에 페이지 상호작용이 제한적일 수 있다.
SSR된 HTML과 클라이언트에서 React가 관리하는 DOM이 일치하지 않으면 문제가 생길 수 있다.</p>
<h2 id="정리">정리</h2>
<p>React에서 Hydration은 SSR된 HTML을 클라이언트 측에서 동적으로 활성화하는 과정이다.
덕분에 빠른 초기 로딩과 클라이언트 측 상호작용을 동시에 처리할 수 있으나, 문제 예방을 위해 서버와 클라이언트 간의 HTML 일치를 보장하는 것이 중요하겠다.</p>
<hr />
<p>next를 공부하며 알게 된 개념이라 해당 글과 겹치는 부분이 있을 수 있지만
React 관점에서 한 번 정리해 본 것에 의의를 둔다.</p>