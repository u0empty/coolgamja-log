<h2 id="📱앱-발행하기">📱앱 발행하기</h2>
<h3 id="bundle-id-생성">Bundle ID 생성</h3>
<ul>
<li><code>android/app/build.gradle</code> 파일에 있는
<code>applicationId = &quot;com.example.contact_app&quot;</code> 이 기존 Bundle ID</li>
<li>프로젝트 생성 시 자동 생성, <code>com.회사명.앱이름</code> 으로 지어주는데 변경 가능</li>
<li>View &gt; Tool Windows &gt; Terminal
<code>dart pub global activate rename</code> 입력</li>
<li><code>rename setAppName --targets ios,android --value &quot;com.회사명.앱이름&quot;</code> 입력</li>
<li>추후 ios 앱 발행 시 ID에 언더바(<code>_</code>)가 포함되면 문제될 수 있음</li>
</ul>
<h3 id="apk-파일-발행">.apk 파일 발행</h3>
<ul>
<li>File &gt; Project Structure</li>
<li>SDK 버전 선택 &gt; OK</li>
<li>Build &gt; Flutter &gt; Build APK</li>
<li>생성된 .apk 파일을 폰으로 옮기면 바로 설치 가능</li>
<li>말고 플레이스토어에 올리려면 아래 과정 따라가기</li>
</ul>
<h3 id="key-파일-생성">key 파일 생성</h3>
<ul>
<li>터미널에 <code>flutter doctor -v</code> 입력</li>
<li><code>Java binary at:</code> 뒤의 주소 중 <code>bin</code>까지 복사</li>
<li>경로 중 띄어쓰기 포함되어 있는 곳은 큰 따옴표로 묶어두기</li>
<li>key 파일 저장할 폴더 하나 만들기
폴더 안의 내용물이 전부 삭제되므로 반드시 새로운 폴더 생성</li>
<li>아래 폼에 맞게 입력 후 터미널에 입력<pre><code>// 폼
복사해둔경로\keytool -genkey -v -keystore key파일넣을폴더경로\upload-keystore.jks -storetype JKS -keyalg RSA -keysize 2048 -validity 10000 -alias upload
</code></pre></li>
</ul>
<p>// 예시
C:&quot;Program Files&quot;\Android&quot;Android Studio1&quot;\jbr\bin\keytool -genkey -v -keystore C:\flutter_key\upload-keystore.jks -storetype JKS -keyalg RSA -keysize 2048 -validity 10000 -alias upload </p>
<pre><code>
- key 비번 입력 후 폴더 경로와 함께 잘 기억해뒀다가
- 현재 프로젝트의 android 폴더 안에 `key.properties` 생성
- 아래 폼에 맞게 입력하고 저장(원(won) 기호 말고 / 사용)

```dart
// 폼
storePassword=입력한비번1
keyPassword=입력한비번2
keyAlias=upload
storeFile=key파일경로/upload-keystore.jks

// 예시
storePassword=123456
keyPassword=123456
keyAlias=upload
storeFile=C:/flutter_key/upload-keystore.jks</code></pre><ul>
<li>이번엔 android/app/build.gradle 파일 내
<code>android {</code> 바로 전에 아래 코드 네 줄 붙여넣기</li>
</ul>
<pre><code class="language-dart">def keystoreProperties = new Properties()
def keystorePropertiesFile = rootProject.file('key.properties')
if (keystorePropertiesFile.exists()) {
    keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
}

android { ..</code></pre>
<ul>
<li><code>android {}</code> 안쪽, <code>buildTypes {</code> 바로 전에 아래 코드 여덟 줄 붙여넣기</li>
</ul>
<pre><code class="language-dart">signingConfigs {
    release {
        keyAlias keystoreProperties['keyAlias']
        keyPassword keystoreProperties['keyPassword']
        storeFile keystoreProperties['storeFile'] ? file(keystoreProperties['storeFile']) : null
        storePassword keystoreProperties['storePassword']
    }
}</code></pre>
<ul>
<li><code>buildTypes {</code> 안에 <code>debug</code> -&gt; <code>release</code>로 수정<pre><code class="language-dart">buildTypes {
  release {
      signingConfig signingConfigs.release
  }
}</code></pre>
</li>
</ul>
<h3 id="aab-파일-발행">.aab 파일 발행</h3>
<ul>
<li>Build &gt; Flutter &gt; Build App Bundle</li>
<li>이걸 구글 플레이스토어에 등록하면 되는데
이 때 개발자 계정(생성 시 25달러 결제) 필요</li>
<li>우선 비공개로 올려서 앱 테스트 가능</li>
</ul>