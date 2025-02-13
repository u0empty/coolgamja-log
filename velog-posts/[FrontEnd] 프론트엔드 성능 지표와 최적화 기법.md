<p>프론트엔드 성능은 사용자 경험과 직결된다.
로딩 속도가 느리거나 반응성이 떨어지는 서비스는 사용자 이탈률을 높이고, 비즈니스 기회까지 감소시킬 수 있다.
구글과 같은 검색 엔진은 웹사이트 성능을 노출 순위를 정하는 요소로 고려하기 때문에, 성능 최적화는 SEO(검색 엔진 최적화)에도 중요한 영향을 미친다.</p>
<p>즉, 프론트엔드 성능 최적화는 단순히 로딩 속도를 개선하는 것을 넘어, <strong>사용자의 만족도를 높이고, 원활한 상호작용을 보장하는 것</strong>을 목표로 한다.
이번 글에서는 프론트엔드 성능을 객관적으로 평가할 수 있는 지표와, 이를 개선할 수 있는 최적화 기법에 대해 간단히 알아보자.</p>
<h2 id="성능-지표">성능 지표</h2>
<h3 id="first-contentful-paint-fcp">First Contentful Paint (FCP)</h3>
<blockquote>
<p>브라우저가 처음으로 콘텐츠(텍스트, 이미지 등)를 화면에 렌더링하는 시점</p>
</blockquote>
<ul>
<li>사용자가 페이지 로딩을 체감하는 첫 순간이므로 빠른 렌더링이 필요하다.</li>
</ul>
<h3 id="largest-contentful-paint-lcp">Largest Contentful Paint (LCP)</h3>
<blockquote>
<p>가장 큰 콘텐츠(이미지, 비디오, 텍스트 블록 등)가 렌더링되는 시점</p>
</blockquote>
<ul>
<li>LCP가 늦어지면 페이지가 로딩되지 않은 것처럼 보일 수 있다.</li>
</ul>
<h3 id="time-to-interactive-tti">Time to Interactive (TTI)</h3>
<blockquote>
<p>사용자가 페이지와 원활하게 상호작용할 수 있는 시점</p>
</blockquote>
<ul>
<li>자바스크립트 실행이 완료되고 UI가 응답할 준비가 된 순간을 의미한다.</li>
</ul>
<h3 id="total-blocking-time-tbt">Total Blocking Time (TBT)</h3>
<blockquote>
<p>페이지가 사용자의 입력(클릭, 스크롤 등)에 반응하지 못한 시간의 총합</p>
</blockquote>
<ul>
<li>오래걸리는 무거운 작업이 많을수록 TBT가 증가하여 UX를 저하시킨다.</li>
</ul>
<h3 id="cumulative-layout-shift-cls">Cumulative Layout Shift (CLS)</h3>
<blockquote>
<p>페이지 내 요소들이 예기치 않게 이동하는 정도(레이아웃 불안정성)</p>
</blockquote>
<ul>
<li>콘텐츠가 갑자기 이동하면 사용자는 불편함을 느낄 수 밖에 없다.</li>
</ul>
<h2 id="성능-최적화-기법">성능 최적화 기법</h2>
<h3 id="로딩-성능-최적화-fcp-lcp">로딩 성능 최적화 (FCP, LCP)</h3>
<ul>
<li><strong>코드 스플리팅 (Code Splitting)</strong>: Webpack 등의 번들러를 활용하여 필요한 코드만 로드</li>
<li><strong>트리 셰이킹 (Tree Shaking)</strong>: 사용되지 않는 코드 제거</li>
<li><strong>리소스 압축 (Gzip, Brotli)</strong>: 서버에서 파일 크기를 줄여 전송 속도 향상</li>
<li><strong>CDN(Content Delivery Network) 사용</strong>: 정적 리소스를 여러 지역에서 빠르게 제공</li>
<li><strong>브라우저 캐싱 활용</strong>: 자주 사용되는 리소스를 캐시하여 로딩 속도 개선</li>
</ul>
<h3 id="인터랙티브-성능-최적화-tti-tbt">인터랙티브 성능 최적화 (TTI, TBT)</h3>
<ul>
<li><strong>불필요한 JavaScript 실행 최소화</strong> (<code>useMemo</code>, <code>useCallback</code> 활용)</li>
<li><strong>Web Worker 활용</strong>: 무거운 연산을 별도의 스레드에서 처리하여 메인 스레드 부담 감소</li>
<li><strong>Debouncing 및 Throttling 적용</strong>: 불필요한 이벤트 호출 최소화 (스크롤, 입력 등)</li>
<li><strong>크리티컬 렌더링 경로 최적화</strong>: CSS, JS 로딩 순서를 조정하여 중요 콘텐츠 먼저 렌더링</li>
</ul>
<h3 id="렌더링-및-ux-최적화-cls">렌더링 및 UX 최적화 (CLS)</h3>
<ul>
<li><strong>레이아웃 이동 방지</strong>: 이미지, 폰트, 광고 요소의 크기를 미리 지정</li>
<li><strong>Lazy Loading 적용</strong>: 사용자가 볼 때만 이미지/비디오 로드 (<code>loading=&quot;lazy&quot;</code>)</li>
<li><strong>Skeleton UI 적용</strong>: 콘텐츠 로딩 중 사용자에게 시각적 피드백 제공</li>
<li><strong>CSS 애니메이션 최적화</strong>: <code>transform</code>과 <code>opacity</code>를 활용하여 GPU 가속</li>
</ul>
<h3 id="네트워크-및-데이터-최적화">네트워크 및 데이터 최적화</h3>
<ul>
<li><strong>HTTP/2 및 HTTP/3 사용</strong>: 병렬 요청을 효율적으로 처리</li>
<li><strong>데이터 페칭 최적화</strong>: GraphQL, SWR, React Query 등을 사용하여 불필요한 API 요청 최소화</li>
<li><strong>Preload &amp; Prefetch 활용</strong>: 사용자가 방문할 가능성이 높은 페이지나 리소스를 미리 로드</li>
</ul>
<h2 id="성능-지표와-최적화-방법">성능 지표와 최적화 방법</h2>
<table>
<thead>
<tr>
<th>성능 지표</th>
<th>관련 최적화 방법</th>
</tr>
</thead>
<tbody><tr>
<td>FCP</td>
<td>코드 스플리팅, 브라우저 캐싱, CDN 사용</td>
</tr>
<tr>
<td>LCP</td>
<td>이미지 최적화, 서버 응답 속도 개선, 크리티컬 CSS 적용</td>
</tr>
<tr>
<td>TTI</td>
<td>불필요한 JS 최소화, Web Worker, Debouncing/Throttling</td>
</tr>
<tr>
<td>TBT</td>
<td>메인 스레드 작업 최소화, 크리티컬 렌더링 경로 최적화</td>
</tr>
<tr>
<td>CLS</td>
<td>레이아웃 이동 방지, Skeleton UI 적용, Lazy Loading</td>
</tr>
</tbody></table>
<p>웹 성능 최적화는 단순히 로딩 속도를 빠르게 하는 것이 아니라, <strong>사용자 경험을 향상</strong>시키는 핵심 요소이다.
각 성능 지표를 이해하고 적절한 최적화 방법을 적용하자!</p>