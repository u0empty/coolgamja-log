<h2 id="new-연산자"><code>new</code> 연산자</h2>
<p>사용자 정의 객체 타입 또는 내장 객체 타입의 인스턴스를 생성하는 연산자이다.
아래와 같은 형태를 갖는다.</p>
<pre><code class="language-javascript">new constructor[[arguments]]();</code></pre>
<ul>
<li><code>constructor</code>: 객체 인스턴스의 타입을 기술하는 함수</li>
<li><code>arguments</code>: <code>constructor</code>와 함께 호출될 값 목록</li>
</ul>
<p><br />그러니까 대충 이런 식으로 쓰는거다.</p>
<pre><code class="language-javascript">function Mole(name, age, height) {
  this.name = name;
  this.age = age;
  this.height = height;
}

const yubin = new Mole(&quot;yubin&quot;, 25, 165);

console.log(yubin.height); // 165</code></pre>
<h3 id="사용자-정의-객체">사용자 정의 객체</h3>
<p><code>new</code> 연산자는 함수(생성자 함수)를 통해 새로운 객체를 생성할 때 사용한다.
<code>new</code>를 통해 생성된 객체는 해당 함수의 <code>prototype</code>을 상속받는다.
이 때, 생성자 함수 내에서 <code>this</code>는 생성된 새 객체를 가리킨다.</p>
<p>객체를 생성하는 과정을 단계별로 정리하면 다음과 같다.</p>
<ul>
<li>새 객체 생성: <code>new</code>는 먼저 <code>Mole.prototype</code>을 상속하는 새로운 객체를 만든다.</li>
<li>생성자 함수 호출: 생성자 함수 <code>Mole</code>이 호출되고, 그 안의 <code>this</code>는 새로 만들어진 객체를 가리킨다. 생성자 함수에서 속성 등을 설정할 수 있다.</li>
<li>객체 반환: 생성자 함수가 명시적으로 객체를 반환하지 않으면, 기본적으로 생성된 객체를 반환한다.</li>
</ul>
<pre><code class="language-javascript">function Mole(name, age) {
  this.name = name;
  this.age = age;
  this.describe = function () {
    return `This mole is ${this.name}. And she is ${this.age}.`;
  };
}

const myMole = new Mole(&quot;yubin&quot;, &quot;25&quot;);
console.log(myMole.describe()); // &quot;This mole is yubin. And she is 25.&quot;</code></pre>
<p>위 코드에서 <code>new Mole('yubin', '25');</code>가 실행되면, <code>Mole.prototype</code>을 상속하는 새 객체가 생성된다.
<code>Mole</code> 함수가 호출되며, <code>this</code>는 새로 만들어진 객체를 가리킨다. <code>this.name</code>과 <code>this.age</code> 속성에 값이 할당된다.
생성된 객체가 <code>myMole</code> 변수에 할당된다.</p>
<h3 id="속성이-또-다른-객체일-때">속성이 또 다른 객체일 때</h3>
<pre><code class="language-javascript">function Mole(mind) {
  this.mind = mind;
}

function Person(sex, name, mole) {
  this.sex = sex;
  this.name = name;
  this.mole = mole;  // Mole 객체를 속성으로 가짐
  this.describe = function() {
    return `${this.sex} is ${this.name} with ${this.mole.mind} mind.`;
  };
}

let myMole = new Mole('strong');  // Mole 객체 생성
let myPerson = new Person('She', 'yuna', myMole);  // Person 객체 생성, Mole 포함

console.log(myPerson.describe());  // &quot;She is yuna with strong mind.&quot;
</code></pre>
<ol>
<li><code>Mole</code>이라는 객체가 따로 있고, <code>Person</code> 객체는 <code>Mole</code> 객체를 속성으로 가질 수 있다.</li>
<li><code>myMole</code>이라는 <code>Mole</code> 객체를 만들고, 이를 <code>myPerson</code>이라는 <code>Person</code> 객체의 속성으로 전달한다.</li>
</ol>
<h3 id="이전에-정의된-객체에-속성을-추가할-때">이전에 정의된 객체에 속성을 추가할 때</h3>
<pre><code class="language-javascript">function Mole() {}
yuna = new Mole();
yubin = new Mole();

console.log(yuna.run); // undefined

Mole.prototype.run = &quot;Tancheon&quot;;
console.log(yuna.run); // Tancheon

yubin.run = &quot;Hokey&quot;;
console.log(yubin.run); // Hokey

console.log(yuna.__proto__.run); //Tancheon
console.log(yubin.__proto__.run); //Tancheon
console.log(yuna.run); // Tancheon
console.log(yubin.run); // Hokey</code></pre>
<p>공유 속성을 추가할 때는 <code>.prototype</code> 속성을 사용한다. 이는 객체 타입의 인스턴스 하나에만 적용되는 것이 아니라 이 함수로 생성하는 모든 객체와 공유하는 속성을 정의하게 된다.</p>
<p>이와 다르게 한 객체에 추가한 속성은 다른 객체들에게는 영향을 주지 않는다.
동일한 타입의 모든 객체들에게 새로운 속성을 추가하려면, <code>Mole</code> 객체 타입의 정의에 이 속성을 추가해야한다.</p>
<p>이렇게 <code>new</code> 연산자를 통해 다양한 객체를 생성하고, 속성으로 다른 객체를 포함하는 방식으로 객체 지향 프로그래밍을 구현할 수 있다.</p>
<h2 id="summary">Summary</h2>
<p>JavaScript의 <code>new</code>는 사용자 정의 객체 타입 또는 객체 타입의 인스턴스를 생성하는 연산자 입니다. <code>new</code>는 해당 함수의 <code>prototype</code>을 상속받는 새로운 객체를 생성합니다. <code>new</code> 연산자를 통해 다양한 객체를 생성하고 <code>prototype</code>으로 속성들을 제어하여 객체 지향 프로그래밍을 구현할 수 있습니다.</p>
<h2 id="reference">Reference</h2>
<p><a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/new">new operator | mdn web docs</a></p>