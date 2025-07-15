<h2 id="프로젝트-초기-세팅">프로젝트 초기 세팅</h2>
<h3 id="프로젝트-생성">프로젝트 생성</h3>
<ul>
<li>File &gt; New &gt; New Flutter Project</li>
<li>Flutter SDK Path 확인</li>
<li>프로젝트명 작명 &gt; Create</li>
</ul>
<h3 id="lint-끄기">lint 끄기</h3>
<p><code>analysis_options.yaml</code> 파일 내 <code>rules:</code> 밑에 코드 추가</p>
<pre><code class="language-dart">rules:
  prefer_typing_uninitialized_variables: false
  prefer_const_constructors_in_immutables: false
  prefer_const_constructors: false
  avoid_print: false
  prefer_const_literals_to_create_immutables: false</code></pre>
<p><code>const</code> 부분은 재랜더링을 줄임, 앱 발행 전 true 시도해보기</p>
<h3 id="maindart">main.dart</h3>
<p>죄다 지우고 stless 위젯 대충 만들어서 시작
MaterialApp은 미리 빼두는게 편할듯</p>
<pre><code class="language-dart">import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(home: MyApp()));
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold();
  }
}</code></pre>
<h2 id="스타일-분리-themedata">스타일 분리: Themedata()</h2>
<h3 id="사용법">사용법</h3>
<pre><code class="language-dart">void main() {
  runApp(
    MaterialApp(
      home: MyApp(),
      theme: ThemeData(
        iconTheme: IconThemeData(color: Colors.blue),
        appBarTheme: AppBarTheme(color: Colors.grey),
      ),
    ),
  );
}</code></pre>
<h3 id="특징">특징</h3>
<ul>
<li>위젯 본인과 가장 가까운 스타일을 먼저 적용</li>
<li>복잡한 위젯(규칙X, 찾아보며 습득)은 <strong>복잡한위젯Theme()</strong> 에 넣어야 먹을 때가 있음
ex) <code>IconThemeData(color: Colors.blue)</code>이 있어도 <code>appBar: AppBar(actions: [Icon(Icons.star)]),</code> 속의 star는 blue가 아님</li>
</ul>
<h3 id="themedata-디자인-반영안됨">ThemeData 디자인 반영안됨</h3>
<h4 id="기존-코드">기존 코드</h4>
<pre><code class="language-dart">theme: ThemeData(
  iconTheme: IconThemeData(color: Colors.amber),
  appBarTheme: AppBarTheme(color: Colors.grey),
),</code></pre>
<h4 id="생김새">생김새<img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/5a5585fa-8cbb-4284-b523-f3606834199a/image.png" /></h4>
<h4 id="변경-코드">변경 코드</h4>
<pre><code class="language-dart">theme: ThemeData(
  iconTheme: IconThemeData(color: Colors.amber),
  appBarTheme: AppBarTheme(
    color: Colors.grey,
    actionsIconTheme: IconThemeData(color: Colors.amber),
  ),
),</code></pre>
<h4 id="생김새-1">생김새<img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/f28fb7cc-eac8-47cb-b79f-24e0938fc3cf/image.png" /></h4>
<h3 id="textthemedata-활용">TextThemeData 활용</h3>
<ul>
<li>Text()는 bodyText2를 사용하는 등 내부적으로 정의된 값 존재</li>
<li>전체 Text 설정이라면 ThemeData 안에 넣어도 되지만 <code>var text1 = TextStyle(); Text('', style: text1)</code> 처럼 변수로 빼서 쓰는 게 나을지도</li>
</ul>