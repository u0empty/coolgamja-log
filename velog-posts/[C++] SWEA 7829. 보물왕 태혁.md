<h2 id="🌽-문제">🌽 <a href="https://swexpertacademy.com/main/code/problem/problemSubmitHistory.do?contestProbId=AWtInr3auH0DFASy">문제</a></h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/b8809535-31ba-492e-9fc9-c30edfcadc67/image.png" /></p>
<h2 id="🥕-입출력">🥕 입출력</h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/bdbcf94f-7ada-41b0-8128-95bc9ad9ee59/image.png" /></p>
<h2 id="🥔-풀이">🥔 풀이</h2>
<p>입력받은 n개의 약수들 중 가장 작은 수와 가장 큰 수의 곱을 출력한다.
약수의 성질이 그렇다.</p>
<h2 id="🥬-코드">🥬 코드</h2>
<pre><code class="language-cpp">#include &lt;iostream&gt;
#include &lt;algorithm&gt;
#include &lt;vector&gt;
using namespace std;

int main() {
    ios::sync_with_stdio(0);
    cin.tie(0);

    int t, n;
    cin &gt;&gt; t;
    for (int i = 1; i &lt;= t; i++) {
        cout &lt;&lt; &quot;#&quot; &lt;&lt; i &lt;&lt; &quot; &quot;;
        cin &gt;&gt; n;
        vector&lt;int&gt; v(n);
        for (int j = 0; j &lt; n; j++) cin &gt;&gt; v[j];
        sort(v.begin(), v.end());
        cout &lt;&lt; v[0] * v[n - 1] &lt;&lt; &quot;\n&quot;;
    }

    return 0;
}</code></pre>
<h2 id="🥜-채점">🥜 채점</h2>
<p>난이도가 왜이래</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/3e2d5d1e-7453-4632-a2bd-299728ad5f71/image.png" /></p>