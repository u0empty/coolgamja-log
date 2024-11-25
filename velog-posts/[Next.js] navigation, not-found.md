<h2 id="복습">복습</h2>
<p>Next.js는 프레임워크다.
우리가 올바른 폴더 안에 올바른 파일에 코드를 작성하면, 갸가 가져다가 쓰는거다.
저번에는 <code>npm init -y</code>로 만든 <code>package.json</code> 파일로 <code>node.js</code> 프로젝트를 생성하고 <code>npm install next@latest react@latest react-dom@latest</code>로 이거 저거 설치를 해줬다.
<code>script</code> 에 <code>dev : next dev</code>를 작성한 뒤 app 폴더 안에 <code>page.tsx</code>를 만들어 고 안에 Tomato 컴포넌트를 만들어뒀다.
여기서 토마토보다 중요한 점은 <code>export default</code>된 <code>react</code> 컴포넌트여야 한다는 것.
어떤 라이브러리도 import 하지 않고, <code>npm run dev</code>로 next를 실행했더니 <code>layout.tsx</code> 파일을 찾다가 지가 하나 만든 다음 localhost: 3000에 내가 만든 토마토 컴포넌트를 렌더링 했다.
<code>next</code>가 실행되어 있는 상태에서, <code>layout.tsx</code>를 삭제해보자. 놀란 <code>next</code>가 금방 다시 만들어준다.</p>
<h2 id="파일-시스템과-라우팅">파일 시스템과 라우팅</h2>
<p><code>react-router</code>는 사용자가 url에 접속하면 그에 맞는 컴포넌트를 렌더링하는 방식으로 동작했고, 제법 번거로운 일이다.</p>
<pre><code>/ ----&gt; &lt;Home /&gt;
/about-us ----&gt; &lt;AboutUs /&gt;
/movies/:id ----&gt; &lt;Movie /&gt;</code></pre><p>next에서는 파일 시스템을 통해 url을 표현한다.
저번에 만든 app은 root이다. localhost:3000에 루트(/)를 입려하면, 루트이자 홈으로 돌아간다.
<strong>만약 내가 about-us url을 만들고 싶다면, app 폴더 내에 about-us 폴더를 만들어주면 된다.</strong>
이 폴더를 만들어줌으로써 next에게, 이 폴더명이 잠재적으로 하나의 페이지가 될 수 있다는 것을 알려주는 것이 된다.
그렇다고해서, 아직 페이지인 것은 아니다. <code>localhost:3000/about-us</code> 에 들어가보면, 아래와 같은 404 화면이 나타난다. 그 페이지에 렌더링할 UI를 만들어주지 않았기 때문이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/33383ed7-612b-431e-8017-87ae2b4972e3/image.png" /></p>
<p><code>app/page.tsx</code>를 만들었던 것처럼, <code>about-us/page.tsx</code>를 만들자.</p>
<pre><code>export default function AboutUs() {
  return &lt;h1&gt;About us!&lt;/h1&gt;;
}</code></pre><p>이런 컴포넌트를 export한 뒤 404가 떴던 그 주소로 돌아가보면, 원하는 화면을 만날 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/229ef5e6-3d24-4082-8200-af353a1e3838/image.png" /></p>
<p>폴더명을 원하는 url로 지정하고, <code>page.tsx</code>로 UI를 만들어주면 된다.
모든 폴더마다 <code>page.tsx</code>가 있을 필요는 없다.
예를 들어, about-us 밑에 company 폴더를 만들고, 그 밑에 바로 <code>sales/page.tsx</code>를 생성한다면 <code>http://localhost:3000/about-us/company/sales</code> 내에 해당 컴포넌트가 렌더링된다.
<code>-/company</code>에 접근하려고 한다면, 아까와 같은 404 페이지가 뜬다.
company 폴더 안에는 page가 없기 때문이다.
즉, company는 경로의 일부분으로만 사용된 것이다.</p>
<p>그렇담 잠시 궁금한 점, app 폴더 내에 page.tsx 외의 파일을 만들어도 될까?
된다.</p>
<p>page.tsx 외에는 실제 경로에 포함되지도 렌더링 되지도 않는다.
app 내에 components 라는 폴더를 만들고, 그 안에 comp.tsx를 생성했다고 하자.
아까 만든 AboutUs 컴포넌트 위에 <code>import comp from &quot;./componentes/comp&quot;;</code>를 넣어주고, return문에 comp를 포함시킨다면, 렌더링은 된다.
그렇지만 components라는 경로가 생기진 않는다.</p>
<p>중요한 것은 page.tsx만이 사용자가 해당 url에 접근했을 때 보이는 모든 것이라는 점이다.</p>
<h2 id="not-foundtsx">not-found.tsx</h2>
<p>지정하지 않은 url에 접속하면, 404 화면이 나타난다.
app 밑에 <code>not-found.tsx</code>를 하나 만들어보자.</p>
<pre><code>export default function NotFound() {
  return &lt;h1&gt;Not found!&lt;/h1&gt;;
}
</code></pre><p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/4c951108-4e23-4c03-97e6-d27fcd1013dc/image.png" /></p>
<p>얼라리!
결국 없는 url에 접근했을 때 보여주는 파일이 <code>not-found.tsx</code>이다.</p>
<h2 id="상단-navigation-bar-구현하기">상단 navigation bar 구현하기</h2>
<p>app과 같은 레벨에 components 폴더를 파고, 그 안에 navigation.tsx를 생성하자.
아래와 같이 작성하되, a 태그는 사용하지 않는다.
이것은 브라우저의 네비게이션을 사용하는 방법이고, 우리가 하려는 건 프레임워크의 네비게이션을 사용하는 것이다.
<code>&lt;a href=&quot;&quot; /&gt;</code> 대신, <code>Link</code> 컴포넌트를 <code>next/link</code>에서 import하여 사용한다.</p>
<pre><code>import Link from &quot;next/link&quot;;

export default function Navigation() {
  return (
    &lt;nav&gt;
      &lt;ul&gt;
        &lt;li&gt;
          &lt;Link href=&quot;/&quot;&gt;Home&lt;/Link&gt;
        &lt;/li&gt;
        &lt;li&gt;
          &lt;Link href=&quot;/about-us&quot;&gt;About Us&lt;/Link&gt;
        &lt;/li&gt;
      &lt;/ul&gt;
    &lt;/nav&gt;
  );
}</code></pre><p>이제, app 밑의 page로 가서 아까 만든 Navigation을 추가하자.</p>
<pre><code>import Navigation from &quot;../components/navigations&quot;;

export default function Tomato() {
  return (
    &lt;div&gt;
      &lt;Navigation /&gt;
      &lt;h1&gt;Hello!&lt;/h1&gt;
    &lt;/div&gt;
  );
}</code></pre><p>about-us 밑의 page와 not-found에도 똑같이 추가해주자.</p>
<pre><code>import Navigation from &quot;../../components/navigations&quot;;

export default function AboutUs() {
  return (
    &lt;div&gt;
      &lt;Navigation /&gt;
      &lt;h1&gt;About us!&lt;/h1&gt;
    &lt;/div&gt;
  );
}</code></pre><pre><code>import Navigation from &quot;../components/navigations&quot;;

export default function NotFound() {
  return (
    &lt;div&gt;
      &lt;Navigation /&gt;
      &lt;h1&gt;Not found!&lt;/h1&gt;
    &lt;/div&gt;
  );
}</code></pre><p>복붙하는 모냥새가 뭔가 깨름칙하지만, client와 server component를 배우기 전이므로 잠자코 따라해본다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/6ee9b830-fc03-4468-bcf7-615f082ffff2/image.png" /></p>
<p>우와
진짜 몬생긴 네비게이션 바가 생겼다.
일단 두고, 유저가 Home에 있으면 Home에 있다는 표시를, About Us에 있을 땐 거기 있음을 알려주는 기능을 추가해보자.</p>
<p>next에는 url에 대한 정보를 알려주는 hook들을 제공한다. router 접근도 가능하다.
nagigation 파일에서 usePathname이라는 hook을 사용해보자.
path name이란 유저가 현재 머물고 있는 url이다.</p>
<pre><code>import Link from &quot;next/link&quot;;
import { usePathname } from &quot;next/navigation&quot;; // &lt;--- !

export default function Navigation() {
  const path = usePathname(); // &lt;--- !
  console.log(path); // &lt;--- !

  return (
    &lt;nav&gt;
      &lt;ul&gt;
        &lt;li&gt;
          &lt;Link href=&quot;/&quot;&gt;Home&lt;/Link&gt;
        &lt;/li&gt;
        &lt;li&gt;
          &lt;Link href=&quot;/about-us&quot;&gt;About Us&lt;/Link&gt;
        &lt;/li&gt;
      &lt;/ul&gt;
    &lt;/nav&gt;
  );
}</code></pre><p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/f31187e3-f2a7-47fd-9fe3-3b6e034975a5/image.png" /></p>
<p>It only works in a Client Component 랜다.
맨 윗 줄에 <code>&quot;use client&quot;</code>를 추가해주자.
어랍쇼 에러가 사라졌다!
콘솔창에도 제대로 나타난다. 싱기</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/6c4b0634-3d62-40c4-935f-f97b0cd0d739/image.png" /></p>
<p>아까 하려고 했던 path 옆에 이모지 심기는 아래와 같이 작성할 수 있다.</p>
<pre><code>      &lt;ul&gt;
        &lt;li&gt;
          &lt;Link href=&quot;/&quot;&gt;Home&lt;/Link&gt; {path === &quot;/&quot; ? &quot;✨&quot; : &quot;&quot;}
        &lt;/li&gt;
        &lt;li&gt;
          &lt;Link href=&quot;/about-us&quot;&gt;About Us&lt;/Link&gt;{&quot; &quot;}
          {path === &quot;/about-us&quot; ? &quot;✨&quot; : &quot;&quot;}
        &lt;/li&gt;
      &lt;/ul&gt;</code></pre><p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/a6fd05f6-5f10-46da-81ec-8403921e2255/image.png" /></p>
<p>굿!</p>
<p>무슨일이 일어났는가는 다음에 더 살펴보도록 하자.
컴터 업데이트 에약을 걸어놨걸랑</p>
<h2 id="reference">Reference</h2>
<p>니꼬쌤 NextJs 강의!</p>