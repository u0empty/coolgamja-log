<h2 id="얼라리">얼라리</h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/7029cee4-96ba-4fdf-a890-814166ca420b/image.png" /></p>
<p>생전 처음 보는 에러 메세지가 떴다.
(아니었음)</p>
<h2 id="에러-발생-조건">에러 발생 조건</h2>
<ol>
<li>잘못된 CSS 구문</li>
</ol>
<ul>
<li>CSS에서 사용할 수 없는 값이나 구조를 작성했을 때 발생한다.</li>
<li>잘못된 선택자, 누락된 중괄호 등</li>
</ul>
<ol start="2">
<li>템플릿 리터럴 내 동적 값 처리 문제</li>
</ol>
<ul>
<li>${}를 사용하는 템플릿 리터럴 내에서 변수를 잘못 사용했거나 구문 오류가 있는 경우 발생한다.</li>
</ul>
<ol start="3">
<li>CSS 문법 규칙 위반</li>
</ol>
<ul>
<li>@media, @keyframes 등에서 규칙이 올바르게 작성되지 않았을 때 발생한다.</li>
</ul>
<h2 id="해결">해결(?)</h2>
<p>하여간 뭐가 틀렸다는거구나 하고 여러 번 살펴보다가
CSS문 중 한 줄에 세미콜론이 없다는 걸 깨달았다.
굉장히 허무</p>