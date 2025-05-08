<h2 id="🌽-문제">🌽 <a href="https://school.programmers.co.kr/learn/courses/30/lessons/87694">문제</a></h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/0aceefc4-7f15-43ab-934f-a6c4d80db341/image.png" /><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/319fad09-eeb1-4f94-923b-148a1cd80bf0/image.png" /></p>
<h2 id="🥔-풀이">🥔 풀이</h2>
<p>좌표를 두 배로 사용해야 아래와 같은 문제를 방지할 수 있다고 한다.</p>
<ol>
<li>사각형들이 붙어있거나 겹치는 경우</li>
<li>사각형 내부의 겉모서리만 밟고 지나가야 할 때</li>
<li>대각선 통과가 가능하게 되어 BFS가 잘못된 길을 허용하는 경우</li>
</ol>
<p><code>auto&amp; r: rectangle</code> 이런거 잘 써먹고 싶은데 맨날 까먹는다.
<code>auto [x, y] = q.front()</code> 이건 기억해냈다.</p>
<p>마지막에 <code>visited</code> 값 원상복구하는 것 잊지 않기..
이 문제 다시 푸는 것도 잊지 않기..</p>
<h2 id="🥬-코드">🥬 코드</h2>
<pre><code class="language-cpp">#include &lt;algorithm&gt;
#include &lt;vector&gt;
#include &lt;queue&gt;

using namespace std;

int dx[4] = {0, 1, 0, -1};
int dy[4] = {-1, 0, 1, 0};

int solution(vector&lt;vector&lt;int&gt;&gt; rectangle, int characterX, int characterY, int itemX, int itemY) {
    int map[102][102] = {0};
    int visited[102][102] = {0};

    for (auto&amp; r : rectangle) {
        int x1 = r[0] * 2, y1 = r[1] * 2;
        int x2 = r[2] * 2, y2 = r[3] * 2;

        for (int i = x1; i &lt;= x2; i++) {
            for (int j = y1; j &lt;= y2; j++) {
                map[i][j] = 1;
            }
        }
    }

    for (auto&amp; r : rectangle) {
        int x1 = r[0] * 2 + 1, y1 = r[1] * 2 + 1;
        int x2 = r[2] * 2 - 1, y2 = r[3] * 2 - 1;

        for (int i = x1; i &lt;= x2; i++) {
            for (int j = y1; j &lt;= y2; j++) {
                map[i][j] = 0;
            }
        }
    }

    queue&lt;pair&lt;int, int&gt;&gt; q;
    q.push({characterX * 2, characterY * 2});
    visited[characterX * 2][characterY * 2] = 1;

    while (!q.empty()) {
        auto [x, y] = q.front(); q.pop();

        if (x == itemX * 2 &amp;&amp; y == itemY * 2) {
            return (visited[x][y] - 1) / 2;
        }

        for (int dir = 0; dir &lt; 4; dir++) {
            int nx = x + dx[dir];
            int ny = y + dy[dir];

            if (nx &lt; 0 || ny &lt; 0 || nx &gt;= 102 || ny &gt;= 102) continue;
            if (!map[nx][ny] || visited[nx][ny]) continue;

            visited[nx][ny] = visited[x][y] + 1;
            q.push({nx, ny});
        }
    }

    return 0;
}</code></pre>
<h2 id="🥜-채점">🥜 채점</h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/2e17e811-38bc-4535-a2c5-a906cdafb6d3/image.png" /></p>