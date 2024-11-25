<p>웹 페이지 제작 시 모든 브라우저에서 페이지의 깨짐 없이, 의도한 대로 표시되도록 하는 작업을 말한다.</p>
<p>브라우저별로 CSS 처리 방식이나 JavaScript 엔진의 차이가 있기 때문에,
크로스 브라우징을 고려하지 않으면 특정 브라우저에서 레이아웃이 깨지거나 기능이 제대로 동작하지 않을 수 있다.
따라서 다양한 브라우저 환경에서 동일한 사용자 경험을 제공하기 위해 크로스 브라우징은 필수적이다.</p>
<h2 id="크로스-브라우징-호환성-보장-방법">크로스 브라우징 호환성 보장 방법</h2>
<h3 id="1-css-reset-normalize">1. CSS Reset, Normalize</h3>
<p>각 브라우저는 고유의 기본 스타일을 가지고 있어 스타일링을 전혀 하지 않은 HTML이라 할지라도 최소한의 형태를 보장한다.
그래서 CSS를 통일하지 않고 프로젝트를 진행하게 되면 어떤 브라우저에서는 의도한 디자인이 뜨지만 다른 브라우저에서는 그렇지 않는 이슈가 발생한다.
이를 해결하기 위해 사용되는 것이 <code>Normalize</code>나 <code>Reset</code>이다.</p>
<p><code>CSS Reset</code>은 브라우저가 기본적으로 설정한 스타일을 0, 없는 상태로 맹그른거다.
아래 사이트를 참고하자.</p>
<pre><code>HTML5 Doctor Reset CSS : http://html5doctor.com/html-5-reset-stylesheet/
css-wipe : https://github.com/stackcss/css-wipe
Reset CSS(Eric Meyer's CSS reset) : http://meyerweb.com/eric/tools/css/reset/
Tinyreset-tiny CSS reset for the modern web : https://github.com/shankariyerr/tinyreset</code></pre><p>모든 것을 reset하고 시작하기 때문에 고려해야 할 변수가 적고, 작업 속도 측면에서 효율적이지만 오히려 코드의 길이를 늘리고, 유용한 스타일까지도 함께 제거하기 때문에 비효율적일 수 있다.</p>
<p>기존의 모든 스타일을 제거하는 Reset과 달리 <code>Normalize</code>는 이를 유지하고 어느 정도 유용한 스타일들은 이용하려는 스타일링 방법이다.
아래 사이트를 참고하자.</p>
<pre><code>Normalize.css : http://necolas.github.io/normalize.css/</code></pre><p>Reset과 다르게 github을 통해 지속적인 업데이트가 이루어지고 있기 때문에 비교적 안정성이 높다.
하지만 명확한 가이드가 없어 진입 장벽이 높다는 게 단점이라면 단점이다.</p>
<pre><code class="language-css">/* CSS Reset */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* Normalize.css */
@import &quot;https://cdnjs.cloudflare.com/ajax/libs/normalize/8.0.1/normalize.min.css&quot;;</code></pre>
<h3 id="2-css-vendor-prefix">2. CSS Vendor Prefix</h3>
<p>특정 브라우저에서만 제공되는 스타일이 있을 수 있다.
그러한 스타일을 사용할 때 <code>-webkit-</code> (Chrome, Safari), <code>-moz-</code> (Firefox), <code>-o-</code> (Opera), <code>-ms-</code> (Internet Explorer) 등의 접두사를 붙여주면 된다.</p>
<pre><code class="language-css">.rounded-box {
  -webkit-border-radius: 10px; /* Safari, Chrome */
  -moz-border-radius: 10px; /* Firefox */
  border-radius: 10px; /* Standard */
}</code></pre>
<h3 id="3-polyfill">3. Polyfill</h3>
<p>구형 브라우저에는 <code>Promise</code>나 <code>Set</code> 객체가 없는 경우가 있다.
<code>Array.prototype.at()</code> API는 Chrome 92 이상에서만 지원된다.
브라우저에 따라 제대로 작동하기도, 작동하지 않기도 하는 코드가 있다는건데 이는 확실히 사용자 경험을 해치는 요인이 된다.</p>
<p>이 때 <strong>Polyfill</strong>을 통해 신규 JavaScript API를 구형 브라우저에서도 사용할 수 있도록 만들어줄 수 있다.
대부분의 Polyfill은 아래와 같이 이미 브라우저에 포함되어 있는지 체크하고, 없으면 값을 채워주는 형태로 동작한다.</p>
<pre><code>Array.prototype.at = Array.prototype.at ?? /* Array.prototype.at에 대한 자체 구현 */;</code></pre><p>위 스크립트를 실행한 이후에는, 구형 브라우저에서도 안전하게 <code>[1, 2, 3].at(-1)</code> 코드를 실행할 수 있다.
표준적으로 사용되는 Polyfill들은 <code>core-js</code> 레포에 모여 있다.</p>
<pre><code>import 'core-js/actual';</code></pre><p>위 코드를 통해 대부분의 ECMAScript 표준 객체와 메서드를 구형 브라우저에서도 사용할 수 있게 된다.
하지만, Polyfill 스크립트가 많아지면 웹 성능이 떨어진다.</p>
<p>이를 해결하기 위해, Babel의 <code>@babel/preset-env</code> 스마트 프리셋을 이용하여 포함할 Polyfill 스크립트의 범위를 지정할 수 있다.
다만, 이 경우에도 최신 브라우저는 구형 브라우저를 위한 Polyfill을 내려받는다.</p>
<p>이는 User-agent에 따라 동적으로 Polyfill 스크립트를 생성하게 함으로써,
최신 브라우저에서는 아무 Polyfill도 내려주지 않고, 구형 브라우저에서는 필요한 Polyfill만 내려주는 방식으로 브라우저가 꼭 필요한 Polyfill 스크립트만 내려받도록 만들어 개선할 수 있다.</p>
<h3 id="4-점진적-향상progressive-enhancement과-우아한-성능-저하graceful-degradation">4. 점진적 향상(Progressive Enhancement)과 우아한 성능 저하(Graceful Degradation)</h3>
<p><code>점진적 향상(Progressive Enhancement)</code>은 기본적인 기능을 모든 브라우저에서 제공하면서, 최신 브라우저에서는 추가 기능을 경험할 수 있도록 설계하는 방법이다.
계층형으로 발전시키기 때문에 하나의 계층에서는 문제가 거의 없다.
따라서 추가된 기능을 지원할 때에 최소한 이전 계층들에 대해서는 신뢰할 수 있다는 장점을 갖는다.
사용자와 크롤러 모두에게 좋은 접근성을 제공하지만, 많은 시간과 노력을 필요로 한다.</p>
<p><code>우아한 성능 저하(Graceful Degradation)</code>는 점진적 향상과 정반대의 성격을 갖는다.
최신 브라우저에서 최상의 경험을 제공하면서, 구형 브라우저에서는 기능이 제한되더라도 페이지가 작동하도록 설계하는 방법이다.
모바일 최적화 시, 우선 데스크탑을 기준으로 웹 사이트를 개발한 다음 모바일에서도 지원 가능하도록 기능과 디자인을 단계적으로 조절하는 것도 우아한 성능 저하의 원칙을 적용한 것이다.
모든 사람에게 최상의 경험을 제공하는 것이 아니라 최신 버전의 브라우저를 위한 솔루션을 개발하는 것을 목표로 한다.</p>
<p><br /><strong>5. 개발자 도구 및 테스트 도구 활용</strong></p>
<ul>
<li><a href="https://caniuse.com">Can I Use</a>: CSS 사용 범위 확인</li>
<li><a href="https://www.browserstack.com/">BrowserStack</a>, <a href="https://saucelabs.com/">Sauce Labs</a>: 크로스 브라우징 테스트 웹 서비스</li>
<li><a href="https://www.cypress.io/">Cypress</a>: 웹 테스트 자동화 도구</li>
</ul>
<br />

<h3 id="reference">Reference</h3>
<ul>
<li><a href="https://velog.io/@cjy0029/Normalize-Reset-%EB%AD%98%EC%8D%A8%EC%95%BC-%ED%95%A0%EA%B9%8C">Normalize, Reset 뭘써야 할까?</a></li>
<li><a href="https://toss.tech/article/smart-polyfills">똑똑하게 브라우저 Polyfill 관리하기</a></li>
</ul>