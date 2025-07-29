<p>UI가 화면 크기를 넘어갈 때 발생하는 에런 것 같다.
과속방지턱같은게 뜨는데 제법 봐주기 싫게 생겼다.</p>
<h2 id="해결-방법">해결 방법</h2>
<h3 id="image-등-위젯-크기-조정하기">Image 등 위젯 크기 조정하기</h3>
<p>오버플로 안나게 들어있는 위젯들을 쪼만하게 만들어주자</p>
<h3 id="singlechildscrollview로-감싸주기">SingleChildScrollView로 감싸주기</h3>
<pre><code class="language-dart">SingleChildScrollView(
  scrollDirection: Axis.horizontal,
  child: Column(children: []),
)</code></pre>
<h3 id="listview로-감싸주기column">ListView로 감싸주기(Column)</h3>
<pre><code class="language-dart">ListView(
  return Column(children: []);
),</code></pre>
<h3 id="그-외">그 외</h3>
<ul>
<li><code>Expanded</code>로 감싸기(ListView)</li>
<li><code>SizedBox</code>로 감싸기(Container)</li>
</ul>
<br />
뜰 때마다 까먹어서 (내가)바로 찾을 수 있게 태그도 많이 넣어뒀다.