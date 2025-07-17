<p>Navigator, Router 말고 Tab으로 페이지를 분리해보자
TabBar 위젯을 갖다써도 되지만 동적 UI는 처음이니 직접 만들어보기</p>
<h2 id="동적-ui-만들기">동적 UI 만들기</h2>
<ol>
<li>state에 UI(오늘은 tab)의 현재 상태 저장</li>
<li>state에 따라 UI를 어떻게 보일지 작성</li>
<li>유저가 state를 쉽게 조작하도록 만들기</li>
</ol>
<h3 id="1-state에-tab의-현재-상태-저장">1. state에 tab의 현재 상태 저장</h3>
<ul>
<li>기존 위젯이 stless 였다면 stful로 변환하기</li>
<li>state 생성 ex) <code>var tab = 0;</code></li>
</ul>
<h3 id="2-state에-따라-어떤-tab을-노출시킬지-작성">2. state에 따라 어떤 tab을 노출시킬지 작성</h3>
<ul>
<li>if문을 써도 되지만 body를 List로 짜면 편함</li>
<li><code>body: [Text('홈'), Text('샵')][tab]</code></li>
</ul>
<h3 id="3-유저가-state를-쉽게-조작하도록-만들기">3. 유저가 state를 쉽게 조작하도록 만들기</h3>
<ul>
<li>bottomNavigationBar의 구조가 아래와 같다면</li>
</ul>
<h4 id="기존-bottomnavigationbar">기존 bottomNavigationBar</h4>
<pre><code class="language-dart">bottomNavigationBar: BottomNavigationBar(
  items: [
    BottomNavigationBarItem(
      icon: Icon(Icons.home_outlined),
      label: '홈',
    ),
    BottomNavigationBarItem(
      icon: Icon(Icons.shopping_bag_outlined),
      label: '샵',
    ),
  ],
),</code></pre>
<ul>
<li>onTab을 추가하여 tab 값을 변경하자</li>
<li>onTab에는 파라미터 하나를 넣게 되어 있는데 탭 값과 같음</li>
</ul>
<h4 id="ontab이-있는-bottomnavigationbar">onTab이 있는 bottomNavigationBar</h4>
<pre><code class="language-dart">bottomNavigationBar: BottomNavigationBar(
  onTap: (i) {
    setState(() {
      tab = i;
    });
  },
  items: [
    BottomNavigationBarItem(
      icon: Icon(Icons.home_outlined),
      label: '홈',
    ),
    BottomNavigationBarItem(
      icon: Icon(Icons.shopping_bag_outlined),
      label: '샵',
    ),
  ],
),</code></pre>
<h2 id="결과">결과</h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/e7be5ac4-ad29-44c5-a818-e642bc709c50/image.gif" /></p>
<p>TabBar 위젯 말고 PageView 같은 위젯도 사용해보자.
흔히 말하는 Carousel 개발 시 자주 쓰인다.</p>