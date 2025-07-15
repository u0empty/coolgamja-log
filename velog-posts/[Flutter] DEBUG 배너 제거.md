<h2 id="maindart">main.dart</h2>
<p><code>MaterialApp</code>에 <strong>debugShowCheckedModeBanner: false</strong>를 추가하자</p>
<pre><code class="language-dart">MaterialApp(
  debugShowCheckedModeBanner: false,
  ...
)</code></pre>
<h2 id="자잔">자잔</h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/482165e9-b871-4059-ae4a-b0cdf14a1d60/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/dd875817-43e1-4614-9290-56cb3de3952e/image.png" /></p>
<h2 id="debug-배너의-역할">DEBUG 배너의 역할</h2>
<ul>
<li>앱이 Debug 모드(개발 중 실행)로 실행 중임을 시각적으로 알림</li>
<li>릴리스 빌드(배포용)가 아니라는 것을 명확히 구분하기 위함</li>
<li>실수로 Debug 앱을 사용자에게 배포하는 것을 방지하기 위한 개발자 도구</li>
</ul>
<h2 id="flutter-실행-모드-비교">Flutter 실행 모드 비교</h2>
<table>
<thead>
<tr>
<th>모드</th>
<th>특징</th>
<th>용도</th>
<th>디버깅 가능 여부</th>
</tr>
</thead>
<tbody><tr>
<td><strong>Debug</strong></td>
<td>- 코드 hot reload 가능<br />- assert 작동<br />- &quot;DEBUG&quot; 배너 표시</td>
<td>개발 중 기능 구현 및 테스트</td>
<td>가능</td>
</tr>
<tr>
<td><strong>Profile</strong></td>
<td>- 성능 분석 가능<br />- 로그 및 CPU 사용량 등 모니터링<br />- 디버깅 제한</td>
<td>성능 측정, 배포 전 최적화 단계</td>
<td>제한적 가능</td>
</tr>
<tr>
<td><strong>Release</strong></td>
<td>- 최적화된 바이너리 생성<br />- 디버깅 기능 제거<br />- 배너 없음</td>
<td>실제 배포용 (플레이/앱스토어)</td>
<td>불가능</td>
</tr>
</tbody></table>