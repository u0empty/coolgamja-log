<h2 id="이렇게">이렇게</h2>
<p>페이지가 많은 경우 Tab, Nivigator 말고 아래와 같이 <code>route</code>를 활용할 수 있다.</p>
<pre><code class="language-dart">void main() {
  runApp(
    MaterialApp(
      initialRoute: '/',
      routes: {
        '/': (c) =&gt; Text('초기 페이지'),
        '/detail': (c) =&gt; Text('다음 페이지')
      },
  );
}</code></pre>
<h3 id="initialroute">initialRoute</h3>
<p>앱 로드시 이동할 <code>route</code> 지정</p>
<h3 id="routes">routes</h3>
<p><code>route</code>별 보여줄 페이지(위젯) 지정</p>
<h2 id="navigatorpushnamedcontext-route">Navigator.pushNamed(context, route)</h2>
<p><code>Navigator.pushNamed(context, '/detail')</code>
이거 쓰면 유저들이 버튼 눌렀을 때 다른 라우트로 이동시킬 수 있음</p>
<h2 id="주의">주의</h2>
<p>맨 처음부터 <code>route</code> 나누는 작업은 불필요할 것 같고 페이지 많아지거나 복잡한 앱일 경우 거때 나눠주면 좋을듯 state 이런거 끼면 굉장히 복잡해질 가능성 농hoo</p>