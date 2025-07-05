<h3 id="앱-개발">앱 개발</h3>
<ul>
<li>Kotlin: Android</li>
<li>Swift: iOS</li>
<li>Flutter, React Natice: Both</li>
</ul>
<h3 id="flutter--react-native">Flutter &gt;&gt; React Native</h3>
<ul>
<li>하나의 코드베이스</li>
<li>성능 굿</li>
<li>Dart 하나로 레이아웃, 기능, 스타일 커버</li>
</ul>
<h3 id="lint-관련-warning-제거">Lint 관련 warning 제거</h3>
<pre><code class="language-dart">rules:
  prefer_typing_uninitialized_variables: false
  prefer_const_constructors_in_immutables: false
  prefer_const_constructors: false
  avoid_print: false
  prefer_const_literals_to_create_immutables: false</code></pre>
<h3 id="한글을-에러로-인식할-때">한글을 에러로 인식할 때</h3>
<p>File &gt; Settings &gt; Editor &gt; Inspections &gt; 상단 Profile을 Default로 선택 &gt; Proofreading &gt; Typo 체크 해제</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/29935cfb-357d-493b-b41b-cb33a21c9fa5/image.png" /></p>
<h3 id="저장-시-자동-코드-포맷팅">저장 시 자동 코드 포맷팅</h3>
<p>file &gt; settings &gt; languates &amp; Frameworks &gt; Flutter &gt; Format on save 체크</p>
<h3 id="단축어">단축어</h3>
<ul>
<li>stless</li>
<li>stful</li>
</ul>
<h3 id="단축키">단축키</h3>
<ul>
<li>ctrl + space: 파라미터 확인</li>
<li>alt + 0: Commit 탭 제어</li>
<li>alt + 4: Run 탭 제어</li>
<li>ctrl + alt + l: 포맷팅</li>
</ul>
<h3 id="이미지-넣기">이미지 넣기</h3>
<ul>
<li>프로젝트 최상단에 assets/ 폴더 만들고 이미지 파일 담기</li>
<li>pubspec.yaml &gt; <code>flutter: assets:</code> &gt; 하단에 <code>- assets/</code> 추가</li>
<li>위젯 내 경로 예시: 'assets/coolgam.png'</li>
</ul>
<h3 id="색상-넣기">색상 넣기</h3>
<ul>
<li>color: Colors.amber</li>
<li>color: Color.fromRGBO(r, g, b, o)</li>
<li>color: Color(0xffffc107)</li>
</ul>
<h3 id="lp-logical-pixel">LP: Logical Pixel</h3>
<ul>
<li>px 안쓰는 이유: 기기마다 픽셀의 절대 크기가 다름</li>
<li>lp: 해상도와 관계없이 일정한 크기를 갖는 추상적인 단위, 화면 크기와 독립적</li>
<li>해상도 낮은 폰에서 lp 하나랑 장치 픽셀 하나가 맞먹는다 치면 해상도 높은 폰에선 lp 하나가 장치 픽셀 2개에 해당될 수도 있는 것</li>
</ul>
<h3 id="처음보는-레이아웃도-쉽게-만드는-방법">처음보는 레이아웃도 쉽게 만드는 방법</h3>
<ol>
<li>디자인 준비</li>
<li>모든걸 최대한 빈틈 없이 네모 박스로 표시하기</li>
<li>가장 바깥 네모 박스부터 코드로 옮기기</li>
<li>가로 세로는 Row와 Column 위젯 사용하기</li>
</ol>
<h3 id="앱-스타일-위젯">앱 스타일 위젯</h3>
<ul>
<li>MaterialApp(): 구글 기본앱 느낌, 커스텀도 이걸로하고 후에 구글물 짜기</li>
<li>Curpentino(): 앱스토어 느낌</li>
</ul>
<h3 id="기본-위젯">기본 위젯</h3>
<ul>
<li>Icon(Icons.-)</li>
<li>Image.asset('path')</li>
<li>Text('', style: TextStyle(..))</li>
<li>TextButton(child: Text('버튼'), onPressed: (){} )</li>
<li>ElevatedButton(child: Text('버튼'), onPressed: (){} )</li>
<li>IconButton(icon: Icon(), onPressed: (){} )</li>
<li>Scaffold(floatingActionButton:
  FloatingActionButton(child: Text('버튼'), onPressed: (){}))</li>
</ul>
<h3 id="레이아웃-위젯">레이아웃 위젯</h3>
<ul>
<li>Row(mainAxisAlignment: .., children: [])</li>
<li>Column(mainAxisAlignment: .., children: [])</li>
<li>ListView(children: [])
SNS 피드 등 긴 목록이 필요할 때 사용
무한 스크롤, 메모리 절약 등 유용함</li>
</ul>
<ul>
<li>ListTile(): 좌측 그림 + 우측 Text 레이아웃<pre><code class="language-dart">ListTile(
  leading: Image.asset('assets/coolgam.png'),
  title: Text('멋감'),
)</code></pre>
</li>
<li>ListView.builder(): 목록 동적 생성<pre><code class="language-dart">ListView.builder(
  itemCount: list.length(),
  itemBuilder: (context, i) {
      return ListTile(
          leading: Image.asset('assets/coolgam.png'),
          title: Text(list[i]),
      )
  }
)</code></pre>
</li>
</ul>
<ul>
<li><p>Flexible(): 여러 박스 배치 시 너비/높이를 고정값 말고 비율로 주고 싶을 때</p>
<pre><code class="language-dart">Row(
    children: [
        Flexible(flex: 1, child: Container(color: Colors.amber)),
        Flexible(flex: 2, child: Container(color: Colors.blue)),
    ]
)</code></pre>
<p>→ 각 1 : 2만큼 차지</p>
</li>
<li><p>Expanded(): 여러 박스 배치 시 하나의 박스만 남은 가로폭 꽉 채우게 만들기</p>
<pre><code class="language-dart">Row(
    children: [
        Expanded(flex: 1, child: Container(color: Colors.amber)),
        Container(width: 50, child: Container(color: Colors.blue)),
    ]
)</code></pre>
</li>
<li><p>Scaffold(
appBar: AppBar(title: ..),
body: ..,
bottomNavigationBar: BottomAppBar(..))</p>
</li>
<li><p>AppBar(
title : Text('제목'),
leading : Icon(Icons.앱바 최좌측 아이콘),
actions : [ Icon(Icons.앱바 최우측 아이콘들), Icon(Icons.-) ])</p>
</li>
</ul>
<h3 id="박스-위젯">박스 위젯</h3>
<ul>
<li>SizedBox(): width, height만 필요한 박스면 이게 가벼우니 이거 쓰기</li>
<li>Container(width: 10, height: 10, color: Colors.amber)
color를 줘야 눈에 보임
width, height가 안먹는 이유: 위치를 안잡아줘서
Center(child: Container(..)) 등</li>
<li>Container(width: double.infinity): 박스폭 가로로 꽉차게</li>
<li>Container(margin: ..): 바깥 여백
근데 이제 <code>EdgeInsets.all(10)이나</code>.fromLTRB(10, 20, 30, 40)` 같이 드럽게 줘야함</li>
<li>Container(padding: ..): 안쪽 여백
Row, Column 말고 Container에만 여백 줄 수 있음
Row에 여백 주려면 Container로(를) 감싸기
padding을 위한 Padding() 위젯도 존재</li>
<li>Container(decoration: BoxDecoration(..))
color, boxShadow, borderRadius 등 중요치 않은 박스 스타일 지정</li>
<li>(복습) Center(child: Container(..)): 중앙정렬</li>
<li>Align(alignment: Alignment..., child: Container(..))
Alignment 뒤에 bottomLeft 등 넣어 박스 정렬</li>
</ul>
<h3 id="커스텀-위젯">커스텀 위젯</h3>
<p>재사용 잦은 UI나 큰 페이지 단위로 커스텀 위젯화</p>
<pre><code class="language-dart">MaterialApp(
  home: Scaffold(
    appBar: AppBar(),
    body: SizedBox( child: Custom() ),
  )
);

class Custom extends StatelessWidget {
  const Custom({super.key});

  @override
  Widget build(BuildContext context) {
    return 따로 뺄 위젯()
  }
}</code></pre>
<h3 id="상태-state">상태: state</h3>
<ul>
<li>StatefulWidget 안에 있는 변수 = state</li>
<li>setState((){ state 변경 코드 })</li>
<li>state 쓰는 위젯은 state 변경되면 재렌더링됨</li>
<li>state 내리기(패륜, 불륜 전송 불가/부모 → 자식만 가능)</li>
</ul>
<h3 id="context">context</h3>
<p>현재 위젯의 조상 위젯들에 대한 정보를 담음, 쉽게 말해 족보 개념</p>
<pre><code class="language-dart">class MyApp extends StatelessWidget {
  ...
  build (context) {
    return MaterialApp(
      home : Scaffold(
        body : Custom()
      )
    );
  }
}

class Custom extends StatelessWidget {
  ...
  build (context) {
    return Text('족보');
  }
}</code></pre>
<p>Custom 위젯 안의 context에는 Scaffold, MaterialApp 정보가 들어있고
MyApp한텐 부모가 없으므로 context에도 암것두 없음</p>
<h3 id="context가-필수인-함수">context가 필수인 함수</h3>
<ul>
<li>Navigator() </li>
<li>Theme.of()</li>
<li>Scaffold.of()</li>
<li>showDialog(): 특히 MaterialApp 정보 필수<pre><code class="language-dart">build (context) {
  return MaterialApp(
    home: Scaffold(
      floatingActionButton: FloatingActionButton(
        onPressed: (){
          showDialog( 
            context: context,
            builder: (context){ return Dialog( child: Text('안녕'), ); },
          );
        },
      ),</code></pre>
이 경우 MaterialApp의 context(정보 없음)를 갖다 쓰게 되므로 에러 발생
→ MaterialApp을 이 부모로 들어있는 context를 하나 만들(MaterialApp을 바깥으로(부모쪽으로) 보내)거나
→ Builder(builder: (context2) {return FAB(.. (context2)(return Dialog(..)))} 사용
→ Builder 쓰면 복잡해지니 응급 시에 사용, 보통 MaterialApp을 바깥으로 빼서 해결</li>
</ul>
<h3 id="기타">기타</h3>
<ul>
<li>좌측 전구: 자동 완성, 감싸기, 변환, 설치 등</li>
</ul>