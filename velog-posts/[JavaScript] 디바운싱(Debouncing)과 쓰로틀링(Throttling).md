<h2 id="개념">개념</h2>
<ul>
<li><strong>디바운싱</strong>: 빈번하게 발생하는 이벤트를 <strong>특정 시간 이후에 한 번만</strong> 실행시키는 최적화 기법</li>
<li><strong>쓰로틀링</strong>: 빈번하게 발생하는 이벤트를 <strong>일정한 간격으로 한 번만</strong> 실행시키는 최적화 기법</li>
</ul>
<p>여기서 말하는 '빈번하게 발생하는 이벤트'의 예로써 검색어를 입력하는 상황을 들 수 있다.
'멋진감자'를 검색하려고 한다면 <code>'ㅁ', '머', '멋', '멋ㅈ', '멋지', '멋진', '멋진ㄱ', '멋진가', '멋진감', '멋진감ㅈ', '멋진감자'</code> 의 과정을 거쳐,
하나의 단어를 타이핑하기 위해 총 11번의 쿼리를 날리게 된다.
유료 API를 사용하고 있다면 비용면에서 문제가 생길 수 있고, 당연히 성능에도 좋지 않은 영향을 끼칠 것이다.</p>
<p>이러한 문제에 대한 대표적인 해결 방법이 <strong>디바운싱</strong>과 <strong>쓰로틀링</strong>이다.</p>
<h2 id="디바운싱debouncing">디바운싱(Debouncing)</h2>
<p>회로를 구성할 때, 전압이 순간적으로 불규칙하게 들어가는 현상을 바운싱 현상이라고 한다.
이 바운싱 현상이 발생하는 시간만큼의 딜레이를 주어 문제를 해결하는 방법인 <strong>디바운싱</strong>에서 유래되었다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/3c4bf26a-2c26-4c00-8aab-1754b6b9819b/image.png" /></p>
<h3 id="구현">구현</h3>
<p>서론에 언급한 검색어 입력 상황에 디바운싱을 적용해보자.
사람들은 보통 검색어를 입력할 때 한번에 타이핑한다.
따라서 input 이벤트가 발생할 때마다 타이머를 설정하고, 일정 시간동안 입력이 없으면 입력이 끝난 것으로 간주하면 된다.
설정한 시간이 지나기 전에 입력이 발생하면, 그 전에 발생한 타이머는 취소하고 새로운 타이머를 재설정하도록 구현할 수 있다.</p>
<pre><code class="language-javascript">const delay = 200;
let timer;

document.querySelector(&quot;#input&quot;).addEventListener(&quot;input&quot;, function (e) {
  clearTimeout(timer);
  timer = setTimeout(() =&gt; {
    console.log(&quot;디바운싱이지요&quot;, e.target.value);
  }, delay);
});</code></pre>
<h2 id="쓰로틀링throttling">쓰로틀링(Throttling)</h2>
<p>쓰로틀링은 엔진의 연료를 조절하는 데 사용되는 레버인 <strong>Throttle</strong>이라는 단어에서 유래되었다.
위에서 언급했듯이, 실행 횟수에 제한을 거는 것이기 때문에 스크롤이 일어날 때 발생하는 이벤트 처리 등 성능 문제를 해결할 때 많이 사용한다.</p>
<h3 id="구현-1">구현</h3>
<p>검색 기능에는 쓰로틀링보다 디바운싱이 더 적합해 보이지만,
중간에 검색 결과를 보여주는 기능이 필요하다면 쓰로틀링도 활용할 수 있겠다.</p>
<p>이번엔 타이머가 설정되어 있으면 아무 동작도 하지 않고, 타이머가 없다면 타이머를 설정한다.
타이머는 일정 시간 후에 스스로를 해제하고, 검색어를 처리하도록 구현하면 된다(console 부분).</p>
<pre><code class="language-javascript">const delay = 200;
let timer;

document.querySelector(&quot;#input&quot;).addEventListener(&quot;input&quot;, function (e) {
  if (!timer) {
    timer = setTimeout(function () {
      timer = null;
      console.log(&quot;쓰로틀링이네요&quot;, e.target.value);
    }, delay);
  }
});</code></pre>
<h2 id="디바운싱-vs-쓰로틀링">디바운싱 vs 쓰로틀링</h2>
<h3 id="디바운싱">디바운싱</h3>
<p>특정 시간 동안 이벤트가 발생하지 않을 때 한 번만 실행된다.
즉, 이전 이벤트를 무시하고 마지막 이벤트가 발생한 이후 일정 시간 동안 추가 이벤트가 발생하지 않아야 실행된다.</p>
<h3 id="활용">활용</h3>
<p>검색창에서 API 호출을 줄일 때, resize 이벤트에서 레이아웃을 계산할 때 사용한다.
검색창에 입력할 때, 디바운싱을 적용해 사용자가 입력을 멈춘 후에만 검색 요청을 보내는 식이다.</p>
<h3 id="쓰로틀링">쓰로틀링</h3>
<p>첫 이벤트가 발생한 이후 일정 간격마다 이벤트를 실행한다.
즉, 이벤트가 지속적으로 발생하더라도 일정한 주기로 실행된다.</p>
<h3 id="활용-1">활용</h3>
<p>무한 스크롤 구현 시 스크롤 이벤트 처리나, 화면 캡처를 주기적으로 수행해야 하는 경우 사용한다.
스크롤 이벤트에 쓰로틀링을 적용하면, 사용자가 페이지를 스크롤할 때 설정한 간격마다 이벤트가 실행되어 브라우저 과부하를 막고 부드럽게 동작되도록 만들 수 있다.</p>
<h2 id="마치며">마치며</h2>
<p>각각의 동작을 이해하는 데 도움이 되는 사진을 첨부한다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/95d445be-5618-4165-aff7-a4455774ee38/image.png" /></p>
<h2 id="정리">정리</h2>
<p>디바운싱은 이벤트 발생이 끝난 후에 동작하는 것이 적합한 경우,
쓰로틀링은 이벤트가 지속적으로 발생할 때 간격을 두고 실행하는 것이 적합한 경우 사용한다.</p>
<h2 id="reference">Reference</h2>
<p><a href="https://url.kr/wxkxmo">디바운싱과 쓰로틀링 이해하기</a>
<a href="https://www.zerocho.com/category/JavaScript/post/59a8e9cb15ac0000182794fa">쓰로틀링과 디바운싱</a>
<a href="https://thrillfighter.tistory.com/597">바운싱 현상</a></p>