<h3 id="maindart">main.dart</h3>
<pre><code class="language-dart">import 'package:flutter/material.dart';

void main() {
  runApp(
    MaterialApp(
      home: MyApp(),
      theme: ThemeData(
        appBarTheme: AppBarTheme(
          elevation: 1,
          titleTextStyle: TextStyle(fontWeight: FontWeight.bold, fontSize: 25),
        ),
      ),
      debugShowCheckedModeBanner: false,
    ),
  );
}

class MyApp extends StatelessWidget {
(생략)</code></pre>
<p>여기서 <code>ThemeData(~)</code>를 잘라 lib 폴더 안에 새롭게 파일 하나를 만들고 붙인다.
만든 파일은 아무렇게나 작명 ex) <code>style.dart</code></p>
<h3 id="분리할-파일">분리할 파일</h3>
<p>에 옮긴 <code>ThemeData(~)</code>는 변수로 선언해주고
맨 끝에 세미콜론(<code>;</code>)을 붙인 뒤
<code>main.dart</code>에 있던 <code>import</code> 문을 갖다 붙인다.
기본 위젯들을 쓰기 위함이다.</p>
<pre><code class="language-dart">import 'package:flutter/material.dart';

var theme = ThemeData(
  appBarTheme: AppBarTheme(
    elevation: 1,
    titleTextStyle: TextStyle(fontWeight: FontWeight.bold, fontSize: 25),
  ),
);</code></pre>
<h3 id="마무리">마무리</h3>
<p>정의한 변수명을 <code>main.dart</code>에서 ThemeData가 있던 곳에 작성하고,
해당 파일의 경로를 import 한다.
나는 자동완성 기능을 사용했는데
<code>import 'style.dart';</code>도
<code>import './style.dart';</code>도 된다.</p>
<pre><code class="language-dart">import 'package:flutter/material.dart';
import 'package:instagram/style.dart';

void main() {
  runApp(
    MaterialApp(home: MyApp(), theme: theme, debugShowCheckedModeBanner: false),
  );
}</code></pre>
<p><code>ThemeData()</code> 뿐만 아니라
다른 모든 긴, 복잡한, 분리 필요한 코드도 요렇게 파일로 빼내어 관리할 수 있다.</p>
<h3 id="import-시-변수-중복-문제-피하기">import 시 변수 중복 문제 피하기</h3>
<ol>
<li><code>as</code> 키워드로 파일 재정의<pre><code class="language-dart">import './style.dart as style';
</code></pre>
</li>
</ol>
<p>(생략)
    MaterialApp(home: MyApp(), theme: style.theme),</p>
<p>```</p>
<ol start="2">
<li>한 파일 내에 여러 변수가 정의된 경우, 다른 파일에서의 사용 막기
→ 변수/함수/클래스명 앞에 언더바(<code>_</code>) 붙이기
ex) <code>var _byeonsoo = ..;</code> </li>
</ol>