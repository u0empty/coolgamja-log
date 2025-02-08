<p><code>call()</code>, <code>apply()</code>, <code>bind()</code>는 JavaScript에서 <code>this</code>를 명확하게 제어할 때 유용한 메서드이다.</p>
<h2 id="this를-명확히-해야-하는-이유"><code>this</code>를 명확히 해야 하는 이유</h2>
<pre><code class="language-javascript">const myObject = {
  value: 10,
  getValue() {
    console.log(this.value);
  },
};

myObject.getValue(); // 10</code></pre>
<p>단순하게 객체의 메소드로 실행하면 <code>this</code>는 명확하다.</p>
<p>그러나 아래처럼 <code>getValue</code> 함수를 다른 변수에 대입해서 새로운 함수를 만들 때 문제가 생긴다.</p>
<pre><code class="language-javascript">const myObject = {
  value: 10,
  getValue() {
    console.log(this.value);
  },
};

const boundFunction = myObject.getValue;
boundFunction(); // undefined</code></pre>
<p><code>boundFunction</code> 이라는 변수에 <code>getValue</code> 함수를 할당할 때 함수의 참조만을 전달하는데, 그렇게 되면 함수 자체가 단독으로 호출되어 <code>this</code>는 전역 객체(브라우저: Window, Nodejs: global)를 참조한다.</p>
<p>따라서 함수 내부의 <code>this</code>는 전역 객체인 <code>window</code>를 가리키고,
<code>this.value</code>가 <code>window.value</code>를 참조하게 된다.
그런데 <code>window</code> 전역객체에는 <code>value</code> 라는 항목이 없으니
<code>undefined</code>를 출력하는 것이다.</p>
<p>이렇게 <code>this</code>가 명확하지 않음으로써 발생하는 문제를
<code>call</code>, <code>apply</code>, <code>bind</code>로 해결할 수 있다.</p>
<h2 id="call">call()</h2>
<p><code>call()</code> 메서드는 함수를 호출하면서 첫 번째 인자로 <code>this</code>를 지정하고,
이후의 인자를 개별적으로 전달한다.</p>
<pre><code class="language-javascript">function greet(greeting, punctuation) {
  console.log(greeting + &quot;, &quot; + this.name + punctuation);
}

const person = { name: &quot;gamja&quot; };

greet.call(person, &quot;Hello&quot;, &quot;!&quot;); // Hello, gamja!</code></pre>
<p><code>call()</code>을 사용할 땐 첫 번째 인자로 <code>this</code>를 지정하고, 나머지 인자를 각각 전달한다.
또한 호출 시 즉시 실행된다는 특징을 갖는다.</p>
<h2 id="apply">apply()</h2>
<p><code>call()</code>과 거의 동일하다.
다만 인자를 개별적으로 넘기는 대신 <strong>배열로 전달</strong>해야 한다는 점에서 차이가 있다.</p>
<pre><code class="language-javascript">greet.apply(person, [&quot;Hi&quot;, &quot; :)&quot;]); // Hi, gamja :)</code></pre>
<h2 id="bind">bind()</h2>
<p><code>call()</code> 그리고 <code>apply()</code>와 달리, 즉시 실행되지 않고 <strong>새로운 함수를 반환</strong>한다.</p>
<pre><code class="language-javascript">const boundGreet = greet.bind(person, &quot;Hey&quot;, &quot;!&quot;);
boundGreet(); // Hey, gamja!</code></pre>
<p>즉, <code>this</code>를 지정하지만 함수를 즉시 실행하지 않는다.
반환한 새로운 함수는 나중에 실행하거나, 뒤에 <code>()</code>를 붙여 즉시 실행시킬 수 있다.</p>
<pre><code class="language-javascript">const boundGreet = greet.bind(person, &quot;Hey&quot;, &quot;!&quot;)(); // Hey, gamja!</code></pre>
<h2 id="call-vs-apply-vs-bind">call vs apply vs bind</h2>
<p>세 메서드의 차이점을 표로 정리하면 아래와 같다.</p>
<table>
<thead>
<tr>
<th>메서드</th>
<th>즉시 실행 여부</th>
<th>인자 전달 방식</th>
<th>반환 값</th>
</tr>
</thead>
<tbody><tr>
<td><code>call</code></td>
<td>O (즉시 실행)</td>
<td>개별 전달</td>
<td>함수 실행 결과</td>
</tr>
<tr>
<td><code>apply</code></td>
<td>O (즉시 실행)</td>
<td>배열 전달</td>
<td>함수 실행 결과</td>
</tr>
<tr>
<td><code>bind</code></td>
<td>X (새로운 함수 반환)</td>
<td>개별 전달</td>
<td>새로운 함수</td>
</tr>
</tbody></table>
<h2 id="reference">Reference</h2>
<p><a href="https://mycodings.fly.dev/blog/2024-01-01-all-about-javascript-bind-call-apply">자바스크립트 bind, call, apply 완벽 이해</a></p>