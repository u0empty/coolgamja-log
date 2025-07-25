<h2 id="1-cupertinopageroute">1. CupertinoPageRoute</h2>
<pre><code class="language-dart">import 'package:flutter/cupertino.dart';

GestureDetector(
  child: Text(widget.data[i]['user'], style: bold),
  onTap: () {
    Navigator.push(
      context,
      CupertinoPageRoute(builder: (c) =&gt; Profile()),
    );
  },
),</code></pre>
<p><code>MaterialPageRoute</code> 말고 <code>CupertinoPageRoute</code>를 쓰면 페이지 노출 시 우측에서 좌측으로 밀리는 트랜지션을 사용할 수 있다.
<code>import</code>문 필수!</p>
<h2 id="2-pageroutebuilder">2. PageRouteBuilder</h2>
<pre><code class="language-dart">GestureDetector(
  child: Text(widget.data[i]['user'], style: bold),
  onTap: () {
    Navigator.push(
      context,
      PageRouteBuilder(
        pageBuilder: (c, a1, a2) =&gt; Profile(),
        transitionsBuilder: (c, a1, a2, child) =&gt;
          애니메이션위젯(),
      ),
    );
  },
),</code></pre>
<h3 id="transitionsbuilderc-a1-a2-child">transitionsBuilder(c, a1, a2, child)</h3>
<p><code>PageRouteBuilder</code> 쓸 땐 파라미터 세 개가 필요하다.
커스텀 애니메이션을 <code>transitionsBuilder</code>에 넣을 수 있는데
얘는 파라미터 네 개가 필요하다.</p>
<p>네 개 파라미터 중 c는 context고</p>
<p>a1이 젤 중요한데 animation object라고 한다.
애니메이션이 얼마나 진행됐는지 0에서 1사이 숫자로 표현해준다.
페이지 전환 시작시엔 0, 전환이 끝나면 1인 셈이다.</p>
<p>a2도 animation object인데 child 말고 기존 페이지의 진행도를 의미한다.
보통 child에 애니메이션을 주고 싶으니 쓸 일이 많지 않을듯</p>
<p>child는 애니메이션 줄 애고 위 코드같은 경우 Profile이 들어있는 격</p>
<h3 id="transitionsduration">transitionsDuration</h3>
<p>애니메이션 진행 속도를 지정할 수 있다.
예를 들어 <code>transitionsDuration: Duration(miliseconds: 500)</code>는
500밀리초 동안 애니메이션을 동작시키라는 의미다.</p>
<h2 id="애니메이션-위젯">애니메이션 위젯</h2>
<p>이름만 봐도 대충 뭐하는 위젯인지 알 수 있다.
이리저리 사용해보기</p>
<h3 id="fadetransition">FadeTransition</h3>
<p><code>FadeTransition(opacity: a1, child: child)</code></p>
<p>a1이 애니메이션 진행도이므로(0 -&gt; 0.1 -&gt; ... -&gt; 1)
opacity에 주면 a1과 함께 불투명도가 높아지며 Fade-In 효과를 만들어낸다.</p>
<h3 id="slidetransition">SlideTransition</h3>
<pre><code class="language-dart">PageRouteBuilder(
  pageBuilder: (c, a1, a2) =&gt; Profile(),
    transitionsBuilder: (c, a1, a2, child) =&gt;
      SlideTransition(
        position: Tween(
          begin: Offset(-1.0, 0.0),
          end: Offset(0.0, 0.0),
        ).animate(a1),
        child: child,
      ),
),</code></pre>
<p>여기선 <code>begin</code>이 중요한데 slide 애니메이션의 시작 위치를 정할 수 있다.
왼쪽이 x 좌표고 오른쪽이 y 좌표다.
위 코드의 경우 페이지가 좌측에서 우측으로 밀리고, <code>(1.0, 0,0)</code>이라면 그 반대다.
<code>(0.0, -1.0)</code>이면 위에서, <code>(1.0, -1.0)</code>이면 우측 상단 모서리에서 밀려온다.</p>
<h3 id="hero"><a href="https://youtu.be/Be9UH1kXFDw">Hero</a></h3>
<p>페이지에서 게시물 누르면 게시물 내용은 고대로 유지되고 크기만 쑤욱 커지는 그거
짬 날 때 한번 써보기.</p>
<h3 id="그-외">그 외</h3>
<ul>
<li>PositionedTransition</li>
<li>ScaleTransition</li>
<li>RotationTransition</li>
<li>SlideTransition</li>
</ul>