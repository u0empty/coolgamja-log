<h2 id="배열-처리-함수">배열 처리 함수</h2>
<h3 id="함수형-프로그래밍">함수형 프로그래밍</h3>
<p>함수형 프로그래밍은 함수의 출력 값이 오직 함수로 전달된 인자에만 의존하는 프로그래밍 패러다임으로, 동일한 인자를 사용해 함수를 호출하면 항상 같은 결과를 반환한다.
이를 <strong>참조 투명성</strong>이라고 하며, 함수형 프로그래밍의 핵심 개념 중 하나이다.</p>
<p>배열 처리 함수 <code>map()</code>, <code>filter()</code>, <code>reduce()</code>는 배열을 변형하거나 처리할 때, 상태를 변경하지 않고 입력된 배열의 복사본을 기반으로 동작하며, 원본 배열을 변경하지 않기 때문에 <code>순수 함수</code>의 개념에 부합하다.
이를 통해 함수 실행마다 예측 가능한 결과를 얻을 수 있다.</p>
<p>전통적인 명령형 프로그래밍에서는 전역 변수나 로컬 변수를 사용해 상태를 변경하는데, 이는 side-effect를 발생시킬 가능성을 높인다.
함수 실행 결과가 매번 다르면 코드의 동작을 이해하고 디버깅하기 어려워진다.
배열 처리 함수들은 이러한 부수 효과를 제거하면서, 복잡한 로직을 간결하게 구현할 수 있도록 도와준다.</p>
<h2 id="map"><code>map()</code></h2>
<p>클라이언트는 서버로부터 받은 데이터를 변환해 사용하는 경우가 많다.
<code>map</code>은 배열의 각 요소를 다른 값으로 변환하여 새로운 배열을 생성하며, 주로 배열의 요소를 다른 형태로 변환할 때 사용된다.</p>
<h3 id="사용법">사용법</h3>
<p><code>map</code>은 인자로 콜백을 받는다. map이 호출될 때, 이 콜백에 현재 <strong>값의 iteration, iteration의 index</strong> 그리고 <strong>원본 배열</strong>이 주어진다.
map을 위한 optional한 두 번째 인자도 있다. 이는 콜백 내부에서 <strong>this</strong>를 이용하기 위한 값이다.</p>
<pre><code class="language-javascript">const nums = [1, 2, 3];
const doubled = nums.map((num, index, array) =&gt; {
  return num * 2;
});

console.log(doubled); // [2, 4, 6]</code></pre>
<h3 id="예제">예제</h3>
<p>아래 자바스크립트 오브젝트 배열이 있다고 하자.</p>
<pre><code class="language-javascript">const Moles = [
  { id: 1, name: &quot;jomboo&quot;, position: &quot;first&quot; },
  { id: 2, name: &quot;yuna&quot;, position: &quot;second&quot; },
  { id: 3, name: &quot;zhoo&quot;, position: &quot;third&quot; },
  { id: 4, name: &quot;yubin&quot;, position: &quot;na&quot; },
];</code></pre>
<p>name 값만 모아보자.</p>
<pre><code class="language-javascript">const allMoleNames = Moles.map((Mole) =&gt; {
  return Mole.name;
});

console.log(allMoleNames); // [&quot;jomboo&quot;, &quot;yuna&quot;, &quot;zhoo&quot;, &quot;yubin&quot;];</code></pre>
<p>유틸 함수도 껴볼 수 있다.</p>
<pre><code class="language-javascript">const upperCaseMoles = Moles.map(myMoleFunc);

const myMoleFunc = (Mole) =&gt; {
  return Mole.name.toUpperCase();
};

console.log(upperCaseMoles); // [&quot;JOMBOO&quot;,&quot;YUNA&quot;,&quot;ZHOO&quot;,&quot;YUBIN&quot;];</code></pre>
<p>프로퍼티를 삭제하거나 추가해보자.</p>
<pre><code class="language-javascript">const mapped = Moles.map((Mole) =&gt; {
  const { position, ...rest } = Mole;

  return {
    ...rest,
    ThisMoleIs: &quot;CoolAndWarm&quot;,
  };
});

console.log(mapped);
// [
//   { id: 1, name: &quot;jomboo&quot;, ThisMoleIs: &quot;CoolAndWarm&quot; },
//   { id: 2, name: &quot;yuna&quot;, ThisMoleIs: &quot;CoolAndWarm&quot; },
//   { id: 3, name: &quot;zhoo&quot;, ThisMoleIs: &quot;CoolAndWarm&quot; },
//   { id: 4, name: &quot;yubin&quot;, ThisMoleIs: &quot;CoolAndWarm&quot; },
// ];</code></pre>
<h2 id="filter"><code>filter()</code></h2>
<p>배열의 각 요소에 대해 조건을 평가한 후, 조건에 맞는 요소들만을 포함하는 새로운 배열을 생성한다.</p>
<h3 id="사용법-1">사용법</h3>
<p><code>filter</code>는 map과 동일한 인자를 받으며, 비슷하게 동작한다.
유일한 차이점은 콜백 함수가 <code>true</code> 또는 <code>false</code>를 반환하는 것이다.
<code>true</code>를 반환하면 해당 원소가 배열에 남고, <code>false</code>이면 필터링되어 제거된다.</p>
<pre><code class="language-javascript">const nums = [1, 2, 3, 4];
const even = nums.filter((num, index, array) =&gt; {
  return num % 2 === 0;
});

console.log(even); // [2, 4]</code></pre>
<h3 id="예제-1">예제</h3>
<p>간단한 문자열 검색허기</p>
<pre><code class="language-javascript">const strings = [&quot;hello&quot;, &quot;Matt&quot;, &quot;Mastodon&quot;, &quot;Cat&quot;, &quot;Dog&quot;];

const filtered = strings.filter((str) =&gt; {
  return str.includes(&quot;at&quot;);
});

console.log(filtered); // [&quot;Matt&quot;, &quot;Cat&quot;];</code></pre>
<p><code>Moles</code>에서 나를 찾아보자.</p>
<pre><code class="language-javascript">const naMole = Moles.filter((Mole) =&gt; {
  return Mole.position.toUpperCase() === &quot;NA&quot;;
});

console.log(naMole);</code></pre>
<h2 id="reduce"><code>reduce()</code></h2>
<p>배열 하나를 받아서 하나의 값으로 바꿔준다.</p>
<h3 id="사용법-2">사용법</h3>
<p><code>map</code>, <code>filter</code>와 비슷하게 동작한다. 콜백 인자로 <strong>accumulator</strong>를 받는다는 점에서 차이가 있다.
모든 반환 값을 누적하는 역할으로, <code>reduce</code> 함수의 두 번째 인자 값이 accumulator 초기값이다.</p>
<pre><code class="language-javascript">const nums = [1, 2, 3, 4];
const sum = nums.reduce((acc, curr) =&gt; {
  return acc + curr;
}, 0);
const avg = sum / nums.length;

console.log(sum); // 10
console.log(avg); // 2.5</code></pre>
<h3 id="예제-2">예제</h3>
<p>새로운 <code>Moles</code> 자바스크립트 오브젝트 배열을 가져왔다.</p>
<pre><code class="language-javascript">const Moles = [
  { id: 1, name: &quot;jomboo&quot;, team: &quot;fa&quot; },
  { id: 2, name: &quot;yuna&quot;, team: &quot;bi&quot; },
  { id: 3, name: &quot;zhoo&quot;, team: &quot;tb&quot; },
  { id: 4, name: &quot;yubin&quot;, team: &quot;fa&quot; },
];</code></pre>
<p>..어디 들어들있는지 알아보자.</p>
<pre><code class="language-javascript">const obj = Moles.reduce((acc, curr) =&gt; {
  const team = curr.team;
  const teamCount = acc[team] ? acc[team] + 1 : 1;

  return {
    ...acc,
    [team]: teamCount,
  };
}, {});

console.log(obj); // { &quot;fa&quot;: 2, &quot;bi&quot;: 1, &quot;tb&quot;: 1};</code></pre>
<p>새로운 두더지를 영입했다.</p>
<pre><code class="language-javascript">const newMoles = [Moles, [{ id: 5, name: &quot;hanbin&quot;, team: &quot;banggoo&quot; }]];

const flatnewMoles = newMoles.reduce((acc, curr) =&gt; {
  return acc.concat(curr);
}, []);

console.log(flatnewMoles);
// [
//   { id: 1, name: &quot;jomboo&quot;, team: &quot;fa&quot; },
//   { id: 2, name: &quot;yuna&quot;, team: &quot;bi&quot; },
//   { id: 3, name: &quot;zhoo&quot;, team: &quot;tb&quot; },
//   { id: 4, name: &quot;yubin&quot;, team: &quot;fa&quot; },
//   { id: 5, name: &quot;hanbin&quot;, team: &quot;banggoo&quot; },
// ]</code></pre>
<h2 id="map-filter-reduce"><code>map(), filter(), reduce()</code></h2>
<p>위의 세 함수를 연계하여 사용할 수 있다.</p>
<h3 id="사용법-3">사용법</h3>
<p>2의 배수만 필터링하고, 각 요소를 제곱하여, 총합을 구해보자.</p>
<pre><code class="language-javascript">const numbers = [1, 2, 3, 4, 5];

const result = numbers
  .filter((num) =&gt; num % 2 === 0) // 2의 배수 필터링
  .map((num) =&gt; num ** 2) // 각 요소 제곱
  .reduce((acc, curr) =&gt; acc + curr, 0); // 총합 계산

console.log(result); // 20</code></pre>
<h3 id="예제-3">예제</h3>
<p>조금 더 복잡한 배열을 가져왔다. 각각의 노래는 초로 표기된 길이를 갖는다.</p>
<pre><code class="language-javascript">const day6Songs = [
  { id: 1, name: &quot;nothing but&quot;, artist: &quot;Young K&quot;, duration: 208 },
  { id: 2, name: &quot;Unpainted Canvas&quot;, artist: &quot;WONPIL&quot;, duration: 229 },
  { id: 3, name: &quot;How to love&quot;, artist: &quot;Day6&quot;, duration: 204 },
  {
    id: 4,
    name: &quot;Right Through Me&quot;,
    artist: &quot;Day6 (Even of Day)&quot;,
    duration: 218,
  },
];

const btobSongs = [
  { id: 1, name: &quot;SWIMMING&quot;, artist: &quot;임현식&quot;, duration: 261 },
  { id: 2, name: &quot;AT THE END&quot;, artist: &quot;이창섭&quot;, duration: 230 },
  { id: 3, name: &quot;Dear My Dear&quot;, artist: &quot;서은광&quot;, duration: 269 },
  { id: 4, name: &quot;BE SOMEBODY&quot;, artist: &quot;육성재&quot;, duration: 183 },
];</code></pre>
<p>200초가 넘는 모든 노래의 제목을 컴마로 구분하는 배열을 가져와야 한다면?</p>
<pre><code class="language-javascript">const allSongs = [day6Songs, btobSongs];

const songNames = allSongs
  // 배열 평탄화. const allSongs = [...day6Songs, ...btobSongs];와 같다.
  .reduce((acc, curr) =&gt; {
    return acc.concat(curr);
  }, [])
  // 200초 이상 노래 필터링
  .filter((song) =&gt; song.duration &gt; 200)
  // 노래 이름만 추출
  .map((song) =&gt; song.name)
  // 컴마로 구분된 문자열 생성
  .join(&quot;, &quot;);

console.log(songNames); // nothing but, Unpainted Canvas, How to love, Right Through Me, SWIMMING, AT THE END, Dear My Dear</code></pre>
<h3 id="연계하면-뭐가-좋냐">연계하면 뭐가 좋냐</h3>
<p><code>map</code>, <code>filter</code>, <code>reduce</code>를 함께 사용하면 <code>array[i]</code>와 같은 형식보다 현재 값에 직접 접근하기 쉬워진다.
기존 배열의 변화를 방지하여 side-effect를 최소화할 수 있으며, <code>for 문</code>을 관리할 필요가 없어지고 빈 배열을 생성해 push할 필요도 없어진다.
<br /></p>
<h2 id="summary">Summary</h2>
<p>배열 처리 함수는 함수형 프로그래밍의 원칙을 잘 반영하여 side-effect를 최소화하고 코드의 가독성을 향상시키는 데 강점을 가지고 있다. <code>map</code>은 현재 <strong>값의 iteration, iteration의 index, 그리고 원본 배열</strong>을 인자로 받는다. <code>filter</code>는 map과 동일한 인자를 받지만, <strong>반환값이 boolean</strong>이라는 차이가 있다. <code>reduce</code>는 콜백 인자로 모든 반환 값을 누적하는 <strong>accumulator와 accumulator의 초기값</strong>을 인자로 받는다.</p>
<h2 id="reference">Reference</h2>
<ul>
<li><a href="https://medium.com/@joomiguelcunha/learn-map-filter-and-reduce-in-javascript-ea59009593c4">Learn map, filter and reduce in Javascript</a></li>
</ul>