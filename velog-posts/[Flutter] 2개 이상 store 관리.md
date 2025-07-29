<p><code>state</code> 성격별로 <code>store</code>를 여러 개 만들 수 있는데 이 때 생기는 문제</p>
<h3 id="store-하나">store 하나</h3>
<pre><code class="language-dart">void main() {
  runApp(
    ChangeNotifierProvider(
      create: (c) =&gt; Store1(),
      child: MaterialApp(
        home: MyApp(),
        theme: theme,
      ),
    ),
  );
}</code></pre>
<p>여러 <code>store</code>를 모두 <code>ChangeNotifierProvider</code>로 등록해줘야 함
이렇게 여러 <code>store</code>를 사용할 땐 <code>MultiProvider</code>로 기존의 <code>ChangeNotifierProvider</code>를 감싸줘야 한다.</p>
<h3 id="store-두개-이상">store 두개 이상</h3>
<pre><code class="language-dart">void main() {
  runApp(
    MultiProvider(
      providers: [
        ChangeNotifierProvider(create: (c) =&gt; Store1()),
        ChangeNotifierProvider(create: (c) =&gt; Store2()),
      ],
      child: MaterialApp(
        home: MyApp(),
        theme: theme,
      ),
    ),
  );
}</code></pre>
<h3 id="get-요청으로-갖고온-데이터-활용하기">get 요청으로 갖고온 데이터 활용하기</h3>
<p>그럼 이번에는 get 요청으로 가져온 데이터를 <code>store</code> 속 <code>state</code>에 넣는 방법을 알아보자</p>
<p>다른 함수랑 작성, 사용법이 똑같은데 <code>async await</code>만 잘 넣어주면 된다.</p>
<pre><code class="language-dart">class Store1 extends ChangeNotifier {
  var profileImage = [];

  getData() async {
    var result = await http.get(Uri.parse('서버URL'));
    var result2 = jsonDecode(result.body);
    profileImage = result2;
    notifyListeners();
}</code></pre>
<p><code>initState</code> 때 쓴다 치면
깨알복습 <code>initState</code> 쓰려면 위젯이 <code>stful</code>이어야 한다.</p>
<pre><code class="language-dart">void initState() {
  super.initState();
  Future.microtask(() {
    context.read&lt;Store1&gt;().getData();
  });
}</code></pre>
<p><code>context.read&lt;Store1&gt;().getData();</code> 만 쓰게 되면
잠시 뻘건 화면이 떴다가 정상적으로 동작하는 걸 볼 수 있는데
<code>Future.microtask</code> 같은 걸 써서
<code>MicroTask(비동기 작업 외 모든 동기 작업)</code>를 먼저 처리하도록 해야 한다.
<code>MicroTask</code>가 끝나면 나머지 <code>Task</code>들을 처리하는 순서다.</p>