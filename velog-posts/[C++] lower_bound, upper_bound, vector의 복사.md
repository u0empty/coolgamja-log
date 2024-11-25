<h2 id="백준-18870-좌표-압축">백준 18870. 좌표 압축</h2>
<p>N개의 X좌표가 주어지고, X좌표보다 작은 서로 다른 X의 개수를 출력하는 문제다.
이 때 1 ≤ N ≤ 1,000,000 이고 -10^9 ≤ Xi ≤ 10^9 이다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/28b394d0-960f-4827-99e5-3dae1de121a1/image.png" /></p>
<h2 id="lower_bound-upper_bound">lower_bound, upper_bound</h2>
<p>x값, 그 값의 인덱스, 그리고 답을 계산해 저장할 수 있는 pair&lt;pair&lt;int, int&gt;, int&gt;&gt; 벡터를 만들어서 어떻게 풀어보려고 했는데 너무 복잡시러워서 뭔가 또 배울 때가 됐다 하고 찾아본 게 lower_bound다.</p>
<p>짝꿍은 upper_bound이며
둘 다 (first, last) 범위에서 이진탐색으로 원소를 탐색한 뒤</p>
<ul>
<li>lower_bound: 찾는 값 이상의 값이 나오는 첫 위치 반환</li>
<li>upper_bound : 찾는 값을 초과하는 값이 나오는 첫 위치 반환</li>
</ul>
<p>만약 찾고자 하는 값이 없으면 last 주소값을 반환한다.
벡터의 경우 v.end()와 같다.</p>
<p>이진탐색이므로 배열이 오름차순 정렬되어 있어야 하고,
반환값에서 첫 번째 주소를 빼주면 인덱스 값을 받아낼 수 있다.</p>
<h2 id="풀이">풀이</h2>
<p>먼저 원본 벡터를 입력 받고,
원본 벡터를 복사한 벡터를 만든다.
복벡을 정렬한 뒤 중복값을 삭제해 준 다음,
원본 벡터를 돌며 각 값이 복벡의 어느 인덱스에 위치하는지 출력하면 된다.</p>
<h2 id="코드">코드</h2>
<pre><code class="language-cpp">#include &lt;iostream&gt;
#include &lt;algorithm&gt;
#include &lt;vector&gt;

using namespace std;

int main() {
    int n;
    cin &gt;&gt; n;
    vector&lt;int&gt; v(n);
    for (int i = 0; i &lt; n; i++) {
        cin &gt;&gt; v[i];
    }

    vector&lt;int&gt; v2(v.begin(), v.end()); // &lt;---- 복사 방법은 여러 개
    sort(v2.begin(), v2.end());
    v2.erase(unique(v2.begin(), v2.end()), v2.end());

    for (int i = 0; i &lt; n; i++) {
        int ans = lower_bound(v2.begin(), v2.end(), v[i]) - v2.begin();
        cout &lt;&lt; ans &lt;&lt; &quot; &quot;;
    }

    return 0;
}</code></pre>
<h2 id="vector의-복사">vector의 복사</h2>
<p>코드에서는 <code>vector&lt;int&gt; v2(v.begin(), v.end());</code>를 이용했다.
이거 말고도 <code>vector&lt;int&gt; v2 = v;</code> 또는 <code>vector&lt;int&gt; v2(v);</code>를 쓸 수 있는데</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/70d1d24a-4351-4ad9-80cd-a3639bfe4b18/image.png" /></p>
<p>큰 차이는 없지만 <code>begin(), end()</code>가 젤 빨랐고
고 다음이 <code>v2(v)</code>, 제일 느린 게 <code>v2 = v</code> 였다.</p>
<p>문바문일지도 ~</p>