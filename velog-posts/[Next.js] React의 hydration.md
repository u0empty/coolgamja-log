<p>저번 글에서 자스를 비활시키면 벌어지는 HTML 실종 사건을 다뤘다.
마찬가지로 자스 비활 상태에서 a 태그의 href만 사용한 링크를 클릭하면 페이지가 계속해서 새로고침(hard refresh)되며 ui가 바뀐다.</p>
<p>그런데 다시 자스를 활성화하고 링크를 번갈아 클릭해보면, 새로고침은 일어나지 않는다. 이 현상을 React가 hydrated 되었다고 말한다.
<code>&lt;a href=&quot;/&quot;&gt;Home&lt;/a&gt;</code>가 React component로 변환된건데 이게 페이지 전체를 reload 하지 않고 빠르게 navigate 할 수 있게 만들어준다.
더 자세히 살펴보자.</p>
<h2 id="hydration">hydration</h2>
<p>참고로 (전에 만들어 둔) navigation은 이렇게 생겼다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/35921240-5d1a-4989-bbe1-8401ca42245c/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/29ba55db-9ed5-431d-a6ce-8d56cd72f0df/image.png" /></p>
<p>여기서 사용자가 About Us에 접근하려 링크를 클릭하면
우리는 사용자에게 backend에서 생성된, interactive 하지 않은 boring HTML을 일단 보여준다.
사용자가 Happy 할 동안 뒤에서 프레임워크 load를 수행하고,
프레임워크가 initialize 되는 순간 우리의 application이 React App이 되면서 interactive 해지는 것이다.
프레임워크가 load 되어야 hard refresh 없이 client side navigation을 할 수 있게 된다.</p>
<p>만약 프레임워크의 initialize가 아-주 느리다고 가정했을 때,
우리가 만들어 둔 저 네비는 아직 React component가 아니기 때문에 hard refresh가 일어나게 된다.</p>
<p>서론에서 언급한 것처럼,
자스를 비활했더니 네비게이션 이동 시 refresh가 일어났고,
다시 활성화하니 refresh 없이 이동되는 모습으로 이 네비게이션이 자스에 의해 제어되고 있음을 알 수 있다.</p>
<p>이번에는 navigation에 클릭수를 count하는 버튼을 하나 추가해보자.</p>
<pre><code class="language-typescript">const [count, setCount] = useState(0);

&lt;button onClick={() =&gt; setCount((c) =&gt; c + 1)}&gt;{count}&lt;/button&gt;</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/86053164-8a9f-43dd-9ce5-cc81f6cca226/image.gif" /></p>
<p>자스가 활성화되어 있으면 의도한대로 동작하지만,
자스 비활시에는 고고하게 0을 유지하고 있는 버튼을 관찰할 수 있다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/cb2453b8-635e-4c42-9e35-1e9d5e602b31/image.gif" /></p>
<p>React가 버튼에 eventListener를 연결시키지 않았기 때문이다.</p>
<p>(자스는 잊지말고 다시 활성화)
여기서 일어나는 일을 정리하면 아래와 같다.
/about-us에 접근한 사용자는 <code>&lt;button&gt;0&lt;/button&gt;</code>을 받아 happy 하다.
뒤에선 프레임워크 load 후 initialize 한다.
이 때 <code>&lt;button onClick&gt;{count}&lt;/button&gt;</code>으로 변신하여 페이지가 interactive 하게 바뀔 수 있는 것!</p>
<p>이 과정이 hydration 이다.
즉, hydration은 <strong>단순 HTML을 React Application으로 초기화하는 작업</strong>이다.</p>
<h3 id="reference">Reference</h3>
<p>니꼬쌤</p>