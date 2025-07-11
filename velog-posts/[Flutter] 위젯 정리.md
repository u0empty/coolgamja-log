<h2 id="앱-스타일-위젯">앱 스타일 위젯</h2>
<ul>
<li>MaterialApp(): 구글 기본앱 느낌, 커스텀도 이걸로하고 후에 구글물 짜기</li>
<li>Curpentino(): 앱스토어 느낌</li>
</ul>
<h2 id="기본-위젯">기본 위젯</h2>
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
<h3 id="textfield">TextField()</h3>
<p>글자 입력란</p>
<h4 id="아이콘-넣기">아이콘 넣기</h4>
<pre><code class="language-dart">TextField(
  decoration: InputDecoration(
    icon: Icon(Icons.star), // prefixIcon, suffixIcon..
  ),
),</code></pre>
<h4 id="테두리-색-채우기">테두리, 색 채우기</h4>
<pre><code class="language-dart">TextField(
  decoration: InputDecoration(
    icon: Icon(Icons.abc),
    enabledBorder: OutlineInputBorder(
      borderSide: BorderSide(color: Colors.lightBlue, width: 2.0),
      borderRadius: BorderRadius.circular(30),
    ),
    focusedBorder: OutlineInputBorder(
      borderSide: BorderSide(color: Colors.blueAccent, width: 2.0),
      borderRadius: BorderRadius.circular(30),
    ),
    border: OutlineInputBorder(),

    filled: true,
    fillColor: Colors.blue.shade50,
  ),
),</code></pre>
<h4 id="placeholder-">placeholder ?</h4>
<pre><code>TextField(
  decoration: InputDecoration(
    hintText: 'hintText',
    helperText: 'helperText',
    labelText: 'labelText',
    counterText: 'counterText'
  ),
),</code></pre><h2 id="커스텀-위젯">커스텀 위젯</h2>
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
<h2 id="레이아웃-위젯">레이아웃 위젯</h2>
<ul>
<li>Row(mainAxisAlignment: .., children: [])</li>
<li>Column(mainAxisAlignment: .., children: [])</li>
<li>ListView(children: [])
SNS 피드 등 긴 목록이 필요할 때 사용
무한 스크롤, 메모리 절약 등 유용함</li>
<li>Scaffold(
appBar: AppBar(title: ..),
body: ..,
bottomNavigationBar: BottomAppBar(..))</li>
<li>AppBar(
title : Text('제목'),
leading : Icon(Icons.앱바 최좌측 아이콘),
actions : [ Icon(Icons.앱바 최우측 아이콘들), Icon(Icons.-) ])</li>
</ul>
<h3 id="listtile">ListTile()</h3>
<p>좌측 그림 + 우측 Text 레이아웃</p>
<pre><code class="language-dart">ListTile(
    leading: Image.asset('assets/coolgam.png'),
    title: Text('멋감'),
)</code></pre>
<h3 id="listviewbuilder">ListView.builder()</h3>
<p>목록 동적 생성</p>
<pre><code class="language-dart">ListView.builder(
    itemCount: list.length(),
    itemBuilder: (context, i) {
        return ListTile(
            leading: Image.asset('assets/coolgam.png'),
            title: Text(list[i]),
        )
    }
)</code></pre>
<h3 id="flexible">Flexible()</h3>
<p>여러 박스 배치 시 너비/높이를 고정값 말고 비율로 주고 싶을 때</p>
<pre><code class="language-dart">Row(
    children: [
        Flexible(flex: 1, child: Container(color: Colors.amber)),
        Flexible(flex: 2, child: Container(color: Colors.blue)),
    ]
)</code></pre>
<p>→ 각 1 : 2만큼 차지</p>
<h3 id="expanded">Expanded()</h3>
<p>여러 박스 배치 시 하나의 박스만 남은 가로폭 꽉 차게 만들기</p>
<pre><code class="language-dart">Row(
    children: [
        Expanded(flex: 1, child: Container(color: Colors.amber)),
        Container(width: 50, child: Container(color: Colors.blue)),
    ]
)</code></pre>
<h2 id="박스-위젯">박스 위젯</h2>
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