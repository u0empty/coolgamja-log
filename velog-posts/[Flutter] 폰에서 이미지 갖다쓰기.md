<h2 id="설정">설정</h2>
<h3 id="image_picker-설치"><a href="https://pub.dev/packages/image_picker">image_picker</a> 설치</h3>
<pre><code class="language-dart">dependencies:
  image_picker: ^1.1.2</code></pre>
<h3 id="iosrunnerinfoplist">ios/Runner/Info.plist</h3>
<pre><code class="language-dart">&lt;key&gt;NSPhotoLibraryUsageDescription&lt;/key&gt;
&lt;string&gt;사진첩점 쓸게요&lt;/string&gt;
&lt;key&gt;NSCameraUsageDescription&lt;/key&gt;
&lt;string&gt;카메라점 쓸게요&lt;/string&gt;
&lt;key&gt;NSMicrophoneUsageDescription&lt;/key&gt;
&lt;string&gt;마이크점 쓸게요&lt;/string&gt;</code></pre>
<p>이런 걸 <code>&lt;dict&gt;</code> 밑에 넣는다.
사용자에게 허락 팝업 띄울 때 보이는 문구다.</p>
<h3 id="maindart">main.dart</h3>
<pre><code>import 'package:image_picker/image_picker.dart';
import 'dart:io';</code></pre><h2 id="활용">활용</h2>
<p>이미지 업로드 버튼을 누른 사용자에게
접근 권한 요청 팝업을 띄우고 갖다쓴다 정도의 시나리오로 가보자</p>
<p>그전에 안드로이드 미리보기를 하면 카메라로 사진을 찍을수가 있음
녹색사람이 까불까불하는데 냅다 찍어서 갤러리에 사진 저장해두기</p>
<h3 id="일단-기본-사용법">일단 기본 사용법</h3>
<p>사진 말고 카메라 띄우려면 <code>ImageSource.camera</code>
이미지 말고 비디오 고르려면 <code>picker.pickVideo()</code>
여러 이미지 고르려면 <code>picker.pickMultiImage()</code></p>
<pre><code class="language-dart">IconButton(
  onPressed: () async {
    var picker = ImagePicker();
    var image = await picker.pickImage(source: ImageSource.gallery);
  },
  icon: Icon(Icons.add_box_outlined, size: 35),
),</code></pre>
<p>이렇게 하면 고른 이미지가 <code>image</code> 변수에 저장되고
이걸 자유롭게 갖다 쓰기 위해 <code>state</code>(<code>var userImage;</code>) 하나 생성</p>
<pre><code class="language-dart">setState() {userImage = File(image.path)}</code></pre>
<p>요때 주의할 점 사용자가 이미지를 고르지 않았을 수 있으니 <code>null</code> 체크하기</p>
<h3 id="파일-형식으로-이미지-띄우는-법">파일 형식으로 이미지 띄우는 법</h3>
<p><code>Image.asset</code>은 asset 폴더에 있는 이미지 띄울 때
<code>Image.network</code>는 넷상 이미지 띄울 때
<code>Image.file</code>은 파일 경로로 이미지 띄울 때 사용</p>
<h2 id="참고">참고</h2>
<h3 id="photofilters"><a href="https://pub.dev/packages/photofilters/versions">photofilters</a></h3>
<p>인스타 보면 게시물 올릴 때 필터 넣은거 보여주는 그거 만들 때 활용</p>
<h3 id=""></h3>
<h3 id="노란-과속방지턱같은거">노란 과속방지턱같은거</h3>
<p>레이아웃 깨질 때 보이는거</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/ee4effef-9d89-42b8-bda8-32c49cb6efcb/image.png" /></p>
<p><code>resizeToAvoidBottomInset</code> 써보거나
위젯을 아예 새 페이지로 분리해보거나
이미지 크기를 조절해보거나
스크롤바 넣어서 해결해보기</p>
<h3 id="전체-예시-코드">전체 예시 코드</h3>
<pre><code class="language-dart">IconButton(
  onPressed: () async {
    var picker = ImagePicker();
    var image = await picker.pickImage(source: ImageSource.gallery);
    if (image != null) {
      setState(() {
        userImage = File(image.path);
      });
    }

    Navigator.push(
      context,
      MaterialPageRoute(builder: (c) =&gt; Upload(userImage: userImage)),
    );
  icon: Icon(Icons.add_box_outlined, size: 35),
),</code></pre>