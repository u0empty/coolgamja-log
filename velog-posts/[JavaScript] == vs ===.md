<h2 id="-vs--equality-operators"><code>==</code> vs <code>===</code> (Equality Operators)</h2>
<p>각각 느슨한 동등 비교와 엄격한 동등 비교를 위해 사용되는 연산자이다.
비슷해 보이지만 사실은 매우 다른 두 개념을 살펴보자.</p>
<h3 id="-strict-equality-operator"><code>===</code> (Strict Equality Operator)</h3>
<p>엄격한 동등성, 즉 타입과 값이 모두 같은지 비교할 때 사용한다.
<code>==</code> 연산자보다 간단한 논리를 거친 결과를 반환하므로 보다 먼저 보기로 한다.</p>
<p>같은 타입과 같은 값을 가진 것 사이의 비교이다.
모두 <code>true</code>를 반환한다.</p>
<pre><code class="language-javascript">5 === 5;
// true (모두 숫자, 같은 값)

&quot;hello world&quot; === &quot;hello world&quot;;
// true (모두 문자열, 같은 값)

true === true;
// true (모두 불리언, 같은 값)</code></pre>
<p>바로 두 번째 예제로 넘어가보자.</p>
<pre><code class="language-javascript">77 === &quot;77&quot;;
// false (숫자와 문자열, 같은 값)

&quot;cat&quot; === &quot;dog&quot;;
// false (모두 문자열, 다른 값)

false === 0;
// false (불리언과 숫자, 다른 값)</code></pre>
<p>즉, <code>===</code>은 타입과 값 중 하나라도 다르면 두 값이 같지 않다고 판단하여 <code>false</code>를 반환한다.
아주 직관적인 비교 연산자라고 할 수 있겠다.</p>
<h3 id="-abstract-equality-operator"><code>==</code> (Abstract Equality Operator)</h3>
<p>느슨한 동등성을 비교할 때 사용한다.
강제 형변환(type coercion)을 통해 피연산자들을 공통 타입으로 만든 뒤에, 비교 연산을 수행한다.</p>
<p><code>===</code> 연산자와 비교하여 살펴보자.</p>
<pre><code class="language-javascript">77 === &quot;77&quot;; // false
77 == &quot;77&quot;; // true

false === 0; // false
false == 0; // true</code></pre>
<p>이러한 차이는 강제 형변환에서 나타난다.
자바스크립트가 값을 동등한 타입으로 변환한 후에 값을 비교하기 때문이다.
문자열 <code>'77'</code>은 숫자 <code>77</code>로, 숫자 <code>0</code>은 <code>falsy</code>값 <code>false</code>로 변환된 것이다.</p>
<h3 id="falsy-값"><code>Falsy</code> 값</h3>
<p><code>false == 0</code>이 성립하는 이유는 자바스크립트에서 <code>0</code>이란 값이 <code>falsy</code> 값이기 때문이다.
<code>0</code> 이외에 <code>false</code>, <code>&quot;&quot;</code>, <code>null</code>, <code>undefined</code>, <code>NaN</code> 값이 자바스크립트에서 <code>falsy</code> 값에 해당한다.</p>
<p>이번 기회에 아래 비교 규칙들을 암기해두도록 하자.
개인적으론 매번 헷갈리는 것들이다.</p>
<p><code>NaN</code>값이 가장 쉽다.
굉장히 부정적이라고 볼 수 있겄다.</p>
<pre><code class="language-javascript">false == 0; // true
0 == &quot;&quot;; // true
&quot;&quot; == false; // true

null == null; // true
undefined == undefined; // true
null == undefined; // true

NaN == null; // false
NaN == undefined; // false
NaN == NaN; // false</code></pre>
<p>이제 두 변수가 같은지 확인하는, 우리가 일반적으로 원하는 동등 비교 시에는 <code>===</code> 연산자를 사용하기로 하자.</p>
<h2 id="summary">Summary</h2>
<p><code>==</code>과 <code>===</code>는 동등 비교를 위해 사용되는 연산자이다. <code>===</code>은 값과 타입이 모두 일치하는지 엄격하게 비교한다. 반면에 <code>==</code>은 강제 형변환 후에 비교 연산을 수행하기 때문에 비교적 느슨하다. <code>==</code>은 형변환으로 인해 의도치 않은 상황이 발생할 수 있기 때문에 개발자가 원하는 동등 비교 시에는 <code>===</code>를 사용하는 것이 좋다.</p>
<h2 id="reference">Reference</h2>
<p><a href="https://codeburst.io/javascript-double-equals-vs-triple-equals-61d4ce5a121a">JavaScript — Double Equals vs. Triple Equals</a></p>