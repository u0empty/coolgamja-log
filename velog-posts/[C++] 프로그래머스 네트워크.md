<h2 id="🌽-문제">🌽 <a href="https://school.programmers.co.kr/learn/courses/30/lessons/43162">문제</a></h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/c62dc83d-b748-4052-aa20-655ff06df6fd/image.png" /></p>
<h2 id="🥔-풀이">🥔 풀이</h2>
<p>dfs 연습용 난이도 정도 되는 것 같다.
푸는 방법이 생각나서 다행이다.</p>
<p>처음에 냅다 bfs로 풀려다가 틀었다.
0이랑 이어진 컴퓨터만 확인 가능하므로 당연히 안되는 코드다.</p>
<pre><code class="language-cpp">int cnt = n;

q.push(0);
used[0] = true;
.
.
.
if (!used[next] &amp;&amp; com[now][next])
    cnt--;
.
.
.
return cnt;</code></pre>
<p><code>for (int i = 0; i &lt; n; i++) q.push(i)</code>
뭐 이런 창의적으로 그지같은 풀이로도 도전해봤으나 명백한 dfs 문제였다.</p>
<h2 id="🥬-코드">🥬 코드</h2>
<pre><code class="language-cpp">#include &lt;vector&gt;
using namespace std;

vector&lt;bool&gt; used;

void dfs(vector&lt;vector&lt;int&gt;&gt; com, int now) {
    for (int next = 0; next &lt; com.size(); ++next) {
        if (!com[now][next]) continue;
        if (used[next]) continue;
        used[next] = true;
        dfs(com, next);
    }
}

int solution(int n, vector&lt;vector&lt;int&gt;&gt; computers) {
    used.resize(n, false);

    int cnt = 0;
    for (int i = 0; i &lt; n; i++) {
        if (used[i]) continue;
        used[i] = true;
        dfs(computers, i);
        cnt++;
    }
    return cnt;
}</code></pre>
<h2 id="🥜-채점">🥜 채점</h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/0b417af3-e2e0-461a-8362-f14ee9916a12/image.png" /></p>