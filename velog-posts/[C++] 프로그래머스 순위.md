<h2 id="🌽-문제">🌽 <a href="https://school.programmers.co.kr/learn/courses/30/lessons/49191">문제</a></h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/29198cba-2ff2-4077-905b-0c0e34702ab5/image.png" /></p>
<h2 id="🥔-풀이">🥔 풀이</h2>
<ol>
<li>승패 정보를 2차원 그래프에 저장</li>
<li>플로이드-워셜 알고리즘으로 간접 승패 처리</li>
<li>각 선수마다 승패 총합이 n-1이면 순위 확정 가능</li>
<li>조건 만족하는 선수 수를 세어 반환</li>
</ol>
<h2 id="🥬-코드">🥬 코드</h2>
<pre><code class="language-cpp">#include &lt;vector&gt;

using namespace std;

int solution(int n, vector&lt;vector&lt;int&gt;&gt; results) {
    vector&lt;vector&lt;bool&gt;&gt; win(n + 1, vector&lt;bool&gt;(n + 1, false));
    for (const auto&amp; result : results) {
        int w = result[0];
        int l = result[1];
        win[w][l] = true;
    }

    for (int k = 1; k &lt;= n; ++k) {
        for (int i = 1; i &lt;= n; ++i) {
            for (int j = 1; j &lt;= n; ++j) {
                if (win[i][k] &amp;&amp; win[k][j]) {
                    win[i][j] = true;
                }
            }
        }
    }

    int answer = 0;
    for (int i = 1; i &lt;= n; ++i) {
        int cnt = 0;
        for (int j = 1; j &lt;= n; ++j) {
            if (i == j) continue;
            if (win[i][j] || win[j][i]) cnt++;
        }
        if (cnt == n - 1) answer++;
    }

    return answer;
}</code></pre>
<h2 id="🥜-채점">🥜 채점</h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/776f4f2a-b802-4a89-8d11-fa2b58ec98b2/image.png" /></p>