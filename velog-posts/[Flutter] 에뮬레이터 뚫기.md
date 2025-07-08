<h3 id="만세">만세</h3>
<p><a href="https://github.com/flutter/flutter/issues/156558">https://github.com/flutter/flutter/issues/156558</a></p>
<h3 id="상황">상황</h3>
<p>최근 안드로이드 스튜디오로 플러터 맛보기 중
안드로이드 에뮬레이터 실행이 안되는 이슈 발생
아우 포기할까 싶은데 앱 만들건데 테스트를 못하는 게 말이방구
듣고있는 인강 게시판 뒤져보며 이것저것 시도하다가 해결했읍니다</p>
<h3 id="전개">전개</h3>
<ul>
<li>BIOS 설정 들어가서 VT를 활성화해야하는데
삼성 노트북은 VT 지원이 안된다는 글을 여러 개 봄. 조금 절망</li>
<li>귀찮아서 미루다가 삼성 서비스센터 전화 상담 신청
내가 쓰는 모델은 이미 활성화 되어 있다는 사실 확인
BIOS Info랑 작업 관리자 창에서 확인도 시켜주셨다</li>
<li>Setting에서 Android SDK Intel 버전을 다운받으라는데
Intel이 안보여서 이건 스킵</li>
<li>Tools &gt; Device Manager &gt; (+) Create Virtual Device &gt; 
Pixel 5, API 36 설치 &gt; 빌드 &gt; 실패 &gt; 1237120번째 빌드 &gt; 실패</li>
<li>구글링 해보면서 이거저거 지워보고(.bundle/, .cache/..)
GPT 도움도 받아봤는데 노소용</li>
<li>망령처럼 게시판을 떠돌다 찾은 글
되겠나 하며 따라했는데 갑자기 에러 아닌 뭔가 줄줄 말하더니
폰에 앱이 떴다. 성공!</li>
</ul>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/a5250c35-1b4d-4751-90b5-95b791345faa/image.png" /></p>
<h3 id="해결">해결</h3>
<ol>
<li><code>gradle-wrapper.properties</code> 파일에서 gradle 버전 변경
<code>distributionUrl=https\://services.gradle.org/distributions/gradle-8.9-all.zip</code></li>
</ol>
<ol start="2">
<li><code>settings.gradle.kts</code> 혹은 <code>settings.gradle</code> 파일에서 아래와 같이 version 변경
<code>id(&quot;com.android.application&quot;) version &quot;8.7.1&quot; apply false</code></li>
</ol>
<p>8.9 이거랑 8.7.1 요 두 숫자를 바꿔주면 된다.</p>
<h3 id="넉긴점">넉긴점</h3>
<p>원래 인강 듣다가 이런 이슈를 마주치면 외면이 디폴트값이었는데
계속 파면 되는구나 이걸 이제 해내네 싶기도
역시 개발자는 아무나 하는게 아니구나
근데 이제 그게 나는 아닌 것 같다
그래도 생각 말고 그냥 해보기로 한다</p>