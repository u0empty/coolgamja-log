<h2 id="서버">서버</h2>
<ul>
<li>method(GET/POST), url 주면서 데이터 달라하면 주는 프로그램</li>
<li>url은 서버 개발한 넘한테 묻/달라하기</li>
<li>서버 개발은 nodejs나 firebase 참고</li>
</ul>
<h3 id="get">GET</h3>
<p>데이터 읽고 싶을 때</p>
<h3 id="post">POST</h3>
<p>데이터 보내고 싶을 때</p>
<h2 id="테스트">테스트</h2>
<p>강의 상 임시 서버로 GET 요청을 날려보자</p>
<h3 id="패키지-설치">패키지 설치</h3>
<ul>
<li><code>pubspec.yaml</code> &gt; <code>dependencies</code> 밑에 <code>http: ^버전</code></li>
<li>pub get (전구)</li>
</ul>
<h3 id="androidmanifestxml">AndroidManifest.xml</h3>
<p>android &gt; app &gt; src &gt; main &gt; AndroidManifest.xml <code>&lt;application</code> 앞에
<code>&lt;uses-permission android:name=&quot;android.permission.INTERNET&quot; /&gt;</code> 작성</p>
<h3 id="maindart">main.dart</h3>
<p>맨 위에 아래 두 줄 추가</p>
<pre><code class="language-dart">import 'package:http/http.dart' as http;
import 'dart:convert';</code></pre>
<h3 id="get-요청-보내기">GET 요청 보내기</h3>
<ul>
<li>MyApp 위젯이 로드될 때 GET 요청하도록 <code>initState(){}</code> 생성</li>
<li>GET 요청은 시간이 걸리므로 넘어가지 않도록  <code>await</code> 필요</li>
<li>근데 initState에 <code>async</code> 못 붙이니까 GET 함수 따로 빼기</li>
</ul>
<pre><code class="language-dart">getData() async {
  var result = await http.get(
    Uri.parse('서버URL'),
  );
  print(result.body);
}

@override
void initState() {
  super.initState();
  getData();
}</code></pre>
<h3 id="jsondecode">jsonDecode()</h3>
<ul>
<li>큰따옴표로 묶어서 문자처럼 사기친 상태</li>
<li>jsondecode로 가공 편하게 변환 ex) <code>print(jsonDecode(result.body));</code></li>
</ul>
<h2 id="이슈">이슈</h2>
<h3 id="1-null-data">1. null data</h3>
<h4 id="에러-메세지">에러 메세지</h4>
<pre><code>NoSuchMethodError: '[]'
Dynamic call of null.
Receiver: null
Arguments: [0]</code></pre><h4 id="원인">원인</h4>
<ol>
<li>data가 아직 로딩되지 않은 상태 (null/빈 리스트)에서 data[i]에 접근해서</li>
<li>initState에서 비동기 함수 getData()가 실행중일 때, build()가 먼저 호출</li>
</ol>
<h4 id="해결">해결</h4>
<p>→ <code>data == null</code> 또는 <code>data.isEmpty</code> 체크</p>
<pre><code class="language-dart"> return data == null
        ? CircularProgressIndicator()
        : ListView.builder(</code></pre>
<h3 id="2-isdisposed">2. !isDisposed</h3>
<h4 id="에러-메세지-1">에러 메세지</h4>
<pre><code>Assertion failed: !isDisposed
&quot;Trying to render a disposed EngineFlutterView.&quot;</code></pre><h4 id="원인-1">원인</h4>
<p>동기 작업이 완료되었을 때 위젯이 이미 dispose(unmount)된 경우
위젯이 unmount(dispose) 된 후에도 setState()가 호출되면 문제가 됨</p>
<pre><code class="language-dart">void loadData() async {
  var result = await http.get(...);
  setState(() {  // ❗ 요때 위젯이 dispose되었을 수 있음
    data = jsonDecode(result.body);
  });
}</code></pre>
<h4 id="해결-1">해결</h4>
<pre><code class="language-dart">getData() async {
  var result = await http.get(
    Uri.parse('서버URL'),
  );
  if (!mounted) return;
  setState(() {
    data = jsonDecode(result.body);
  });
}</code></pre>
<h2 id="list-map">list, map</h2>
<p>map 안에 map, list 안에 list 등 모든 자료형을 넣기 가능</p>
<h3 id="list">list</h3>
<ul>
<li>형태: [자료1, 자료2...]</li>
<li>읽기: list이름[0]</li>
<li>결과: 자료1</li>
</ul>
<h3 id="map">map</h3>
<ul>
<li>형태: {'이름1': 자료1, '이름2': 자료2...}</li>
<li>읽기: map이름['이름1']</li>
<li>결과: 자료1</li>
</ul>