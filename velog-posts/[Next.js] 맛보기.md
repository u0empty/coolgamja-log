<h2 id="react-vs-nextjs">React vs Next.js</h2>
<p>React는 라이브러리고, Next.js는 프레임워크다.
라이브러리는 코드 내에서 '우리가' 사용하는 것이다.
원하는 아키텍처를 사용하여 원하는 방식으로 코드를 작성한다.
객체 지향이든, 함수 지향 프로그래밍이든, 원하는 언어로 작성할 수 있다.</p>
<p>주식 시장 어플을 만든다고 할 때, 통화 변환이 필요한 경우 우리는 원하는 라이브러리를 설치하여 사용한다. 원하는 구조와 언어로. 라이브러리는 아무것도 결정하지 않는다. 내가 라이브러리를 활용한다.</p>
<p>React는 UI 인터페이스를 빌드하는데 사용하는 라이브러리이다. 반응형 사용자 인터페이스를 구축하기 위해 사용한다. 이 때 우리는 CSS로 Styled-component를 사용할 수도 있고, SAS를 사용할 수도 있다. 라우팅을 위해 React router를 사용하거나 Expo router를 사용할 수 있다. 원하는 폴더명과 파일명을 정할 수 있고, UI 빌드를 위해 React를 사용한다.</p>
<p>반대로, 프레임워크는 우리의 코드를 사용한다. 여러가지 결정을 우리 대신 자동으로 실행한다.
Next.js를 여러 가지 특징을 가지고 있다. Optimization, HTML Streaming, CSS Support, Data Fetching, Router Handlers, Middleware... 이러한 기능을 사용하려면, 우리는 코드를 올바른 위치에 넣기만 하면 된다. 그러면 프레임워크가 우리가 작성한 코드를 가져다가 사용하고, Next.js의 경우 풀스택 웹 어플리케이션을 빌드한다.</p>
<h3 id="nextjs-수동-설치">Next.js 수동 설치</h3>
<p>자동 설치와 수동 설치 중, 머리털 나고 처음 맛보는 김에 수동 설치를 시도해보자.</p>
<ol>
<li><p>프로젝트 폴더 생성</p>
</li>
<li><p><code>code .</code></p>
</li>
<li><p><code>npm init -y</code></p>
</li>
<li><p><code>package.json</code> &gt; <code>&quot;license&quot;: &quot;ISC&quot; -&gt; &quot;MIT&quot;</code></p>
</li>
<li><p><code>npm install react@latest next@latest react-dom@latest</code>
여기서 React는 UI와 다른 모든 것을 구성하고, React-dom은 그것을 브라우저의 DOM에 렌더링하는 역할을 한다. React Native가 ios나 안드로이드 기기에 렌더하는 것처럼.</p>
</li>
<li><p><code>packages.json</code> &gt; <code>&quot;scripts&quot;: { &quot;dev&quot;: &quot;next dev&quot; },</code></p>
</li>
<li><p>새 파일 생성: <code>app/page.tsx</code>
JS를 쓸거라면 .jsx를, TS를 쓸거라면 .tsx를 확장자로 정하자.</p>
</li>
<li><p><code>page.tsx</code>에서 기본적인 export를 실행해보자. 함수명은 중요하지 않다.
.tsx 파일과 <code>&lt;h1&gt;</code>에 뻘건줄이 생기지만 일단은 넘어가자.</p>
<pre><code> export default function Tomato() {
     return &lt;h1&gt;Hello Next&lt;/h1&gt;
 }</code></pre></li>
<li><p><code>npm run dev</code>
Next.js를 실행하는 순간 Next.js 서버가 만들어지고 화면은 <a href="http://localhost:3000/">http://localhost:3000/</a> 이곳에 렌더링된다.
우리가 TS를 사용하고 싶어하는 걸 알고, 필요한 설정들을 알아서 설치해주기 때문에, 위 단계에서 발견됐던 빨간애들도 없어졌다. 짱신기.
<img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/0aaf858b-6107-408a-a75f-932a6d50406d/image.png" /><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/78d8ea74-cb66-4e48-8bb3-15eb9e28783c/image.png" /><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/d7f57721-81d3-4d4d-ac56-4cabb46db531/image.png" /></p>
</li>
<li><p><code>app/layout.tsx</code> 가 생겼다. 뭐얏
console을 보면 알 수 있다. 이 레이아웃은 다음에 더 알아보도록 허자.
<img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/9241e946-7a15-4321-8400-bfe855cb215c/image.png" /></p>
</li>
<li><p>마지막으로, return 문의 텍스트를 변경해보자. 자동으로 새로고침되는 걸 확인할 수 있다.</p>
</li>
</ol>
<h2 id="reference">Reference</h2>
<p>감삼니다 니꼬쌤
<a href="https://nomadcoders.co/nextjs-for-beginners">https://nomadcoders.co/nextjs-for-beginners</a></p>