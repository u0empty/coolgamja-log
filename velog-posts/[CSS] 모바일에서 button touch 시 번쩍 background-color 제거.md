<p><code>&lt;button&gt;</code> 태그로 개발한 토글 버튼이 있다.
근데 요걸 터치할 때마다 번쩍번쩍 아주 그냥 파티가 열리는 현장 발견</p>
<p>아유 정신사나워</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/14dcd3d5-b3c4-4548-86a4-3e02d0866a48/image.gif" /></p>
<p>이 현상은 모바일 브라우저에 적용된 터치 하이라이트 효과다.
<code>-webkit-tap-highlight-color : transparent;</code>
이 코드로 제거할 수 있다.
안된다면 기존에 씌워둔 <code>css</code> 때문일 수 있으니 <code>!important</code>도 시도해보자.</p>
<p>브라우저(특히 WebKit 기반, iOS Safari 등)는 기본적으로 터치 이벤트 시 버튼이나 링크 요소에 하이라이트(흰색 번쩍임) 효과를 제공하는데,
이 속성을 transparent로 설정하여 제거할 수 있다.</p>
<p>버튼은 많이 쓰일테니 <code>global.css</code>에 박아줬다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/b12239f0-bb87-4b71-96ad-fe706568796e/image.gif" /></p>
<p>만족</p>