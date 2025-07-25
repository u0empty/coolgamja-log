<h3 id="text-위젯에-인터렉션-넣기">Text 위젯에 인터렉션 넣기</h3>
<p>유저가 <code>Text()</code> 위젯을 눌렀을 때 상세페이지를 띄우고 싶을 수도 있음
근데 onPressed 같은 게 없으니 이 때 <code>GestureDetector()</code> 위젯으로 싸맨다.</p>
<pre><code class="language-dart">GestureDetector(child: Text('싸매 me'), onTap: (){});</code></pre>
<p><code>onPressed</code> 말고 <code>onTap</code>을 쓸 수 있다.
길게 눌렀을 때 인터렉션 주려면 <code>onLongPress</code>
두 번 눌렀을 때 인터렉션을 주려면 <code>onDoubleTap</code>
핀치(확대 모션)할 때 주려면 <code>onScaleStart</code>
왼쪽으로 스와이프 했을 때 코드 실행하려면 <code>onHorizontalDragStart</code></p>
<p>이런식으로 특정 동작에 따라 코드 실행시킬 때 <code>GestureDetector()</code> 써보기.
상세페이지는 <code>Navigator.push()</code>로 구현해보자.</p>
<pre><code class="language-dart">onTap: () {
  Navigator.push(
    context,
    MaterialPageRoute(builder: (c) =&gt; Text('상세페이지')),
  );
},</code></pre>
<h3 id="결과물">결과물</h3>
<p>우와 생긴거</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/1befb931-def8-4d09-81f7-113741d5b218/image.gif" /></p>