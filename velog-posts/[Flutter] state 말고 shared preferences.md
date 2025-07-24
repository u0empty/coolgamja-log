<p><code>state</code>에 저장한 데이터는 앱 재가동시 휘발된다.
데이터를 저장하기 위한 방법 중 <code>shared preferences</code> 사용법을 배워보자.</p>
<h2 id="0-데이터-보존-방법">0. 데이터 보존 방법</h2>
<ol>
<li>서버로 보내서 DB에 저장 - 중요한 데이터</li>
<li>폰 메모리카드에 저장 - 들 중요한 데이터
요게 <code>shared preferences</code>를 활용하는 방법이다.
유저가 직접 삭제하지 않는 이상 반영구적으로 남아있게 됨</li>
</ol>
<h2 id="1-shared-preferences">1. <a href="https://pub.dev/packages/shared_preferences">shared preferences</a></h2>
<h3 id="설치">설치</h3>
<pre><code class="language-dart">// pubspec.yaml
dependencies:
  shared_preferences: ^2.5.3

// main.dart
import 'dart:convert'; // &lt;- jsonDecode 함수 쓸 때 필요
import 'package:shared_preferences/shared_preferences.dart';</code></pre>
<p>pub get 후에는 앱(emulator)을 종료하고 다시 시작해주자</p>
<h3 id="사용법">사용법</h3>
<h4 id="데이터-저장">데이터 저장</h4>
<p>저장할 땐 <code>storage.setString('데이터이름', 저장할데이터)</code>
그니까 <code>key</code>하고 <code>value</code> 형태로 쓰면 됨</p>
<pre><code class="language-dart">saveData() async {
  var storage = await SharedPreferences.getInstance();
  storage.setString('name', 'John');
}</code></pre>
<h4 id="데이터-출력">데이터 출력</h4>
<p>출력할 땐 <code>storage.getString('데이터이름')</code></p>
<pre><code class="language-dart">saveData() async {
  var storage = await SharedPreferences.getInstance();
  storage.setString('name', 'John');
  var result = storage.getString('name');
  print(result); // John
}</code></pre>
<h4 id="데이터-삭제">데이터 삭제</h4>
<p>삭제할 땐 <code>storage.remove('데이터이름')</code></p>
<h3 id="함수">함수</h3>
<h4 id="데이터-저장-함수">데이터 저장 함수</h4>
<ul>
<li><code>setString('name', 'John')</code></li>
<li><code>setBool('bool', true)</code></li>
<li><code>setInt('int', 1)</code></li>
<li><code>setDouble('double', 2.5)</code></li>
<li><code>setStringList('stringList', ['John1', 'John2'])</code></li>
</ul>
<p><code>map</code> 자료형은 <code>jsonEncode + setString</code> 조합 활용
<code>map</code>에 전부 따옴표 붙여서 <code>JSON</code>으로 가라쳐줌</p>
<pre><code class="language-dart">var storage = await SharedPreferences.getInstance();
var map = {'count': 3};
storage.setString('map', jsonEncode(map));</code></pre>
<h4 id="데이터-호출-함수">데이터 호출 함수</h4>
<ul>
<li><code>getString('name')</code></li>
<li><code>getBool('bool')</code></li>
<li><code>getInt('int')</code></li>
<li><code>getDouble('double')</code></li>
<li><code>getStringList('stringList')</code></li>
</ul>
<p>아까 저장한 <code>map</code>을 일단 갖고와보자</p>
<pre><code class="language-dart">var result = storage.getString('map');
print(result); // {'count': 3}</code></pre>
<p>근데 이거는 꺼내쓰기 어려운(<code>result['count']</code>: 에러) 형태라
<code>jsonDecode</code> 함수가 필요하다.</p>
<pre><code class="language-dart">print(jsonDecode(result)); // Error: The argument type 'String?' can't be assigned to the parameter type 'String' because 'String?' is nullable and 'String' isn't.</code></pre>
<p>그냥 <code>getString</code> 말고 <code>.get('key')</code>도 먹는데 꺼내보면 <code>Object?</code> 요런식의 타입으로 끄내짐. <code>.getString('key')</code>로 꺼내면 <code>String?</code> 이렇게 타입을 좀 더 명확하게 저장할 수 있다.</p>
<p>다시 돌아가서 <code>String</code>인지 <code>null</code>인지 확실히 않아 뜨는 에러를 해결하기 위해 <code>??</code> 써서 <code>null check</code> 해주기.</p>
<pre><code class="language-dart">var result = storage.getString('map') ?? '없어';
print(jsonDecode(result)); // {count: 3}
print(jsonDecode(result)['count']); // 3</code></pre>
<h3 id="활용">활용</h3>
<ul>
<li>기존에 <code>state</code>로 관리했던 데이터를 <code>shared preferences</code>에 넣어두고,
앱을 켤 때 갖고오는 식으로 관리하면 <strong>로드 속도</strong>가 빨라지고 2 서버와 주고받는 <strong>데이터 양</strong>도 줄일 수 있다.</li>
<li>근데 <code>shared preferences</code>에는 문자만 저장 가능하므로 이미지를 저장하고 싶을 땐 network 이미지를 폰에 몰래 저장해주는 패키지 <a href="https://pub.dev/packages/cached_network_image">cached_network_image</a>를 써보자.
매번 다운받는 게 아니라 필요할 때 폰에서 가져와주니 더 빠르다.</li>
</ul>