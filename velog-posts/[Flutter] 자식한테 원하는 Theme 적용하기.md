<p>중간에 어떤 위젯의 자식들은 새로운 Theme을 따르면 좋겠다 싶을 땐
위젯을 <code>Theme()</code>으로 감싸고(전구 활용) <code>data: ThemeData(원하는 Theme)</code> 작성</p>
<h3 id="구조">구조</h3>
<pre><code class="language-dart">void main() {
  runApp(
    MaterialApp(
      theme: ThemeData(
        textTheme: TextTheme(bodyMedium: TextStyle(color: Colors.blue)), // 전체 텍스트 색상: 파랑
      ),
      home: Scaffold(
        body: Center(child: Text('파란색 텍스트')), // 별도 style 없음 → 파랑
      ),
    ),
  );
}</code></pre>
<h3 id="비교">비교</h3>
<pre><code class="language-dart">void main() {
  runApp(
    MaterialApp(
      theme: ThemeData(
        textTheme: TextTheme(bodyMedium: TextStyle(color: Colors.blue)), // 기본 파랑
      ),
      home: Scaffold(
        body: Theme(
          data: ThemeData(
            textTheme: TextTheme(bodyMedium: TextStyle(color: Colors.red)), // 오버라이드 빨강
          ),
          child: Center(child: Text('빨간색 텍스트')), // Theme 위젯 영향 → 빨강
        ),
      ),
    ),
  );
}</code></pre>
<h3 id="원하는-theme-가져오기">원하는 Theme 가져오기</h3>
<p><code>style: Theme.of(context).textTheme.bodyMedium</code>
→ <code>ThemeData() &gt; textTheme &gt; bodyMedium</code> Theme만 적용하라</p>
<p>요런식으로 원하는 ThemeData 안의 내용을 불러올 수 있다.
바꿔말하면 여러 스타일을 정의해두고 <code>Theme.of()</code>로 갖다 쓰기 가능</p>