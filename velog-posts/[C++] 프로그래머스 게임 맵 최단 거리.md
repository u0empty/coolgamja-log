<h2 id="🌽-문제">🌽 <a href="https://school.programmers.co.kr/learn/courses/30/lessons/1844">문제</a></h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/d1e46fb1-b1a5-4bf4-b459-e8cd71235754/image.png" /></p>
<h2 id="🥔-풀이">🥔 풀이</h2>
<p>bfs 연습하기 좋은 기초 문제,,
인데 여전히 한 번에 풀자를 모다는 ~
used로 최단거리를 기록하는 방법을 사용했다.
GPT는 <code>queue</code>에 <code>dist</code>를 포함해서 쓰라고 추천해줬다.</p>
<pre><code>queue&lt;tuple&lt;int, int, int&gt;&gt; q;
q.push({0, 0, 1});

while (!q.empty()) {
    auto [y, x, dist] = q.front();
    q.pop();

    if (y == n - 1 &amp;&amp; x == m - 1) {
        return dist;
    }</code></pre><p>요런식.</p>
<h2 id="🥬-코드">🥬 코드</h2>
<pre><code class="language-cpp">#include&lt;vector&gt;
#include&lt;queue&gt;
using namespace std;

int dy[4] = {-1, 0, 1, 0};
int dx[4] = {0, 1, 0, -1};

int solution(vector&lt;vector&lt;int&gt;&gt; maps) {
    int n = maps.size();
    int m = maps[0].size();

    vector&lt;vector&lt;int&gt;&gt; used(n, vector&lt;int&gt;(m, 0));
    queue&lt;pair&lt;int, int&gt;&gt; q;

    q.push({0, 0});
    used[0][0] = 1;

    while(!q.empty()) {
        int y = q.front().first;
        int x = q.front().second;
        q.pop();

        if (y == n - 1 &amp;&amp; x == m - 1) {
            return used[n - 1][m - 1];
        }

        for (int i = 0; i &lt; 4; ++i) {
            int ny = y + dy[i];
            int nx = x + dx[i];

            if (ny &lt; 0 || nx &lt; 0 || ny &gt;= n || nx &gt;= m) continue;
            if (used[ny][nx] &gt;= 1) continue;
            if (maps[ny][nx] == 0) continue;

            q.push({ny, nx});
            used[ny][nx] = used[y][x] + 1;
        }
    }

    return -1;
}</code></pre>
<h2 id="🥜-채점">🥜 채점</h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/ddfc6ddf-0fef-456d-89f9-acb3dc321aba/image.png" /></p>