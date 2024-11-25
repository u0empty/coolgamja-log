<h2 id="csr-client-side-rendering">CSR (Client Side Rendering)</h2>
<p><strong>렌더링</strong>은 react 코드를 브라우저가 이해할 수 있는 HTML로 바꾸는 것이다.</p>
<p><code>create-react-app</code>을 사용해 react로 생성한 application은 client가 사용자 브라우저에 UI를 구축하는 client side rendering 방식을 사용한다.
이 환경에서 새로고침을 하면, 잠깐 빈 화면이 떴다가 UI가 표시된다.</p>
<p>빈 화면은 사용자가 도착한 시점에서 해당 페이지가 비어있었기 때문이다.
이후 브라우저의 자바스크립트 엔진이 모든 .js 파일을 다운로드하고 react를 실행시킨 뒤 UI를 화면에 띄우는 과정이 전개된다.</p>
<p>그렇다면 자바스크립트가 비활성화되어 있는 사용자는 어떻게 될까?
<code>개발자도구 &gt; Sources &gt; Disable JavaScript</code> 를 활성화 시켜 보자.</p>
<p><strong>'You need to enable JavaScript to run this app'</strong></p>
<p>즉, 자바스크립트 없이는 해당 application을 실행시킬 수 없는 거다.</p>
<p>disable JavaScript 해두는 사람을 본 적이 없긴 하다.
하지만 인터넷 상태가 나쁜 환경에서 해당 사이트에 접속하려 한다면
거 사람은 자바스크립트가 일하는 오랜 시간 동안 빈 화면만을 보게 된다.</p>
<p>빈 페이지는 SEO에도 좋지 않다. 검색 엔진들은 HTML을 열어보기 때문이다.
자바스크립트를 지원하는 크롤러를 운용하는 검색 엔진은 구글과 빙, 그리고 네이버 정도이다. 이외의 검색 엔진들은 보통 자스를 실행시켜보지 않는다.
결국 검색 엔진은 아래 코드만 보게 되는 거다.</p>
<pre><code class="language-html">&lt;noscript&gt;
  You need to enable JavaScript to run this app.
&lt;/noscript&gt;
&lt;div id=&quot;root&quot;&gt;&lt;/div&gt;</code></pre>
<p>next, Gatsby, Remix 등 어떤 프레임워크도 없이 그저 <code>create-react-app</code>으로 만든 application은 이런 식으로 동작한다.</p>
<h2 id="ssr-server-side-rendering">SSR (Server Side Rendering)</h2>
<p>next는 default로 SSR을 사용한다.
비어있던 CSR의 HTML과 달리, 이미 화면에 표시할 HTML을 갖고 있다.
자바스크립트를 비활성화해 봐도, UI 빌드에 아무런 문제가 없다.</p>
<p>next는 우리가 만든 application의 <strong>모든 컴포넌트와 페이지들을 backend에서 render</strong>한다.
사용자에게 어떠한 HTML을 주기 전에 모든 컴포넌트를 render하고 변환된 HTML을 브라우저의 request에 대한 response로 넘겨주는 것이다.</p>
<p><strong>최초 UI 빌드 과정에 react와 자바스크립트가 필요없다</strong>는 점이 SSR 방식의 큰 장점이다.
(이와 관련해 언젠간 hydration 개념도 배워보도록 하자.)</p>
<p>기억해야할 것은 이 SSR이 모든 컴포넌트에 적용된다는 것이다. server component에도, client component에도, <strong><code>&quot;use client&quot;</code>를 갖고있는 컴포넌트에도 모든 컴포넌트는 우선 server side rendering이 된다.</strong></p>
<p><code>&quot;use client&quot;</code>를 포함하는 컴포넌트에 <code>console.log('hello');</code>를 추가하고, 페이지 새로고침을 누르면 <strong>backend server쪽 console에 뜨는 hello</strong>로 확인할 수 있는 사실이다.
<img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/c7bec97c-20d3-403b-ade0-71360a0ccca7/image.png" /></p>
<br />

<h2 id="reference">Reference</h2>
<p>니꼬쌤</p>