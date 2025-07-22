<h2 id="navigator">Navigator</h2>
<h3 id="특징">특징</h3>
<ul>
<li>페이지 이동 시 새로운 페이지가 기존 페이지를 대체하는 웹사이트와 달리 모바일앱에서는 새로운 페이지가 기존 페이지 위에 덮이는 구조</li>
<li>탭과 달리 Stack으로 페이지가 관리되므로 뒤로가기 시 페이지가 걷히는 식</li>
</ul>
<h3 id="사용법">사용법</h3>
<p><code>React</code>의 <code>useRouter</code>랑 비슷하게 <code>.push</code>를 사용한다.</p>
<pre><code class="language-dart">IconButton(
  onPressed: () {Navigator.push(context, route)},
  icon: Icon(Icons.add_box_outlined, size: 35),
),</code></pre>
<ul>
<li>이 때 context에는 MaterialApp 정보가 포함되어야 함</li>
<li>두 번째 파라미터는 route인데 아래와 같이 작성가능</li>
<li><code>return</code> 뒤, 그러니까 <code>Text('New Page')</code> 부분이 새로운 페이지로 뜨는거</li>
<li>길어지면 커스텀 위젯으로 빼는 게 방법 ~</li>
</ul>
<pre><code class="language-dart">MaterialPageRoute(
  builder: (c) {
    return Text('New Page');
  },
),</code></pre>
<h3 id="자란">자란</h3>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/f5b81c0f-557d-4f0a-87f3-800b29025821/image.gif" /></p>
<h3 id="닫기-버튼">닫기 버튼</h3>
<p>새로 열린 페이지를 닫고 싶을 수 있으니 버튼 하나 만들어보자</p>
<pre><code class="language-dart">IconButton(
  onPressed: () {
    Navigator.pop(context);
  },
  icon: Icon(Icons.close),
),</code></pre>
<p>이 때 <code>Navigator.pop</code>에 들어가는 <code>context</code>는
<code>Navigator.push</code>와 마찬가지로 <code>MaterialApp</code> 정보를 포함해야 함</p>
<h2 id="참고-return-생략하기">(참고) return 생략하기</h2>
<p>위의 <code>MaterialPageRoute</code>의 <code>builder</code>에서와 같이 함수 안에 <code>return</code>문 하나밖에 없다면 아래와 같이 화살표 함수로 더 간단히 작성할 수 있다.</p>
<pre><code class="language-dart">MaterialPageRoute(builder: (c) =&gt; Text('New Page')),</code></pre>
<p><code>Arrow Function</code> 인 잉글리시</p>