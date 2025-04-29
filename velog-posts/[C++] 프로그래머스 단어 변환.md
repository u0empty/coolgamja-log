<h2 id="🌽-문제">🌽 <a href="https://school.programmers.co.kr/learn/courses/30/lessons/43163">문제</a></h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/3d39ae16-79b2-445d-912c-a868a995cba2/image.png" /></p>
<h2 id="🥔-풀이">🥔 풀이</h2>
<p>먼저 생각해 낸 DFS보다 BFS로 풀어야 더 빠르다고 한다.
왜 이렇게 감을 못 잡는걸까? 배고픈가보다.
레벨3 답게 2레벨보다 훨 오래 고민했다.</p>
<p>DFS랑 BFS는 풀이를 어떻게 적어야할지 모르겠다.
코드를 보는 게 더 빠를 것 같다.</p>
<p>대신 미래의 내가 또 까먹고 또 찾으러 올 만한;
함수 사용법을 정리하는 게 낫겠다.</p>
<h3 id="1-1-string의-find">1-1. string의 find</h3>
<h4 id="사용법">[사용법]</h4>
<ul>
<li>str.find(찾을 문자열, 찾기 시작할 위치, 찾을 문자열의 길이)</li>
</ul>
<h4 id="반환값">[반환값]</h4>
<ul>
<li>찾으면: 인덱스값</li>
<li>없으면: string::npos</li>
</ul>
<pre><code class="language-cpp">#include &lt;algorithm&gt;

string str = &quot;coolgamja&quot;;

cout &lt;&lt; str.find(&quot;gamja&quot;); // 4
cout &lt;&lt; str.find(&quot;gogooma&quot;); // 18446744073709551615(trash!)

cout &lt;&lt; str.find(&quot;gamja&quot;, 4, 5); // 4
cout &lt;&lt; str.find(&quot;gamja&quot;, 5, 5); // 18446744073709551615(trash!)
cout &lt;&lt; (str.find(&quot;gamja&quot;, 5, 5) == string::npos); // 1(true.)</code></pre>
<h3 id="1-2-algorithm의-find">1-2. algorithm의 find</h3>
<h4 id="사용법-1">[사용법]</h4>
<ul>
<li>find(v.begin(), v.end(), 찾을 값)</li>
<li>find(arr, arr + arr.size(), 찾을 값)</li>
</ul>
<h4 id="반환값-1">[반환값]</h4>
<ul>
<li>찾으면: vector는 찾을 값의 iterator / array는 포인터</li>
<li>없으면: vector는 v.end() / array는 arr.size()</li>
</ul>
<h4 id="특징">[특징]</h4>
<ul>
<li>array와 vector에서 사용</li>
<li>find 반환값에서 범위의 시작값(array/v.begin())을 빼주면
인덱스값(값을 못 찾은 경우 범위의 크기)을 정확히 얻어낼 수 있다.</li>
</ul>
<pre><code class="language-cpp">#include &lt;algorithm&gt;

vector&lt;string&gt; v = {&quot;hi&quot;, &quot;cool&quot;, &quot;gamja&quot;};

auto it = find(v.begin(), v.end(), &quot;gamja&quot;);
cout &lt;&lt; *it; // gamja
cout &lt;&lt; it - v.begin(); // 2

it = find(v.begin(), v.end(), &quot;gogooma&quot;);
cout &lt;&lt; (it == v.end()); // 1
cout &lt;&lt; it - v.begin(); // 3</code></pre>
<pre><code class="language-cpp">#include &lt;algorithm&gt;

int arr[] = {1, 2, 3};
int n = sizeof(arr) / sizeof(arr[0]);
// sizeof(arr)는 바이트 단위 배열 크기로, 여기선 4*3으로 12가 된다.

int* p = find(arr, arr + arr.size(), 3);
cout &lt;&lt; *p; // 3
cout &lt;&lt; p - arr; // 2

p = find(arr, arr + arr.size(), 3);
cout &lt;&lt; *p; // (trash)
cout &lt;&lt; p - arr; // 3</code></pre>
<h3 id="2-vector의-assign">2. vector의 assign</h3>
<h4 id="사용법-2">[사용법]</h4>
<ul>
<li>v.assign(크기, 초기화 값)</li>
</ul>
<pre><code class="language-cpp">#include &lt;vector&gt;

vector&lt;int&gt; v;

v.assign(100, 1e9);</code></pre>
<p>cstring의 memset으로 1e9 초기화를 했다가 문제가 생겨 알게 된 함수.
참고로 cstring memset은 1바이트 단위로 값을 초기화 하므로,
초기화 값으로 0 또는 char type만 사용할 수 있다.</p>
<h2 id="🥬-코드dfs">🥬 코드(DFS)</h2>
<pre><code class="language-cpp">#include &lt;algorithm&gt;
#include &lt;string&gt;
#include &lt;vector&gt;

using namespace std;

vector&lt;bool&gt; visited;
int answer = 1e9;

bool is1Diff(string a, string b) {
    int diff = 0;
    for (int i = 0; i &lt; a.length(); ++i) {
        if (a[i] != b[i]) diff++;
    }
    return diff == 1;
}

void dfs(string now, string target, vector&lt;string&gt; words, int cnt) {
    if (now == target) {
        answer = min(answer, cnt);
        return;
    }

    for (int i = 0; i &lt; words.size(); ++i) {
        if (visited[i]) continue;
        if (is1Diff(now, words[i])) {
            visited[i] = true;
            dfs(words[i], target, words, cnt + 1);
            visited[i] = false;
        }
    }
}

int solution(string begin, string target, vector&lt;string&gt; words) {
    int ti = find(words.begin(), words.end(), target) - words.begin();
    int n = words.size();
    if (ti == n) return 0;

    visited.assign(n, false);

    dfs(begin, target, words, 0);

    return answer == 1e9 ? 0 : answer;
}</code></pre>
<h2 id="🥜-채점dfs">🥜 채점(DFS)</h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/57c3e1bf-494a-4412-86aa-36046691f3e5/image.png" /></p>
<h2 id="🥬-코드bfs">🥬 코드(BFS)</h2>
<pre><code class="language-cpp">#include &lt;algorithm&gt;
#include &lt;string&gt;
#include &lt;vector&gt;
#include &lt;queue&gt;

using namespace std;

bool is1Diff(string a, string b) {
    int diff = 0;
    for (int i = 0; i &lt; a.length(); ++i) {
        if (a[i] != b[i]) diff++;
    }
    return diff == 1;
}

int solution(string begin, string target, vector&lt;string&gt; words) {
    int ti = find(words.begin(), words.end(), target) - words.begin();
    int n = words.size();
    if (ti == n) return 0;

    vector&lt;bool&gt; visited(n, false);
    queue&lt;pair&lt;string, int&gt;&gt; q;
    q.push({begin, 0});

    while (!q.empty()) {
        auto [now, cnt] = q.front();
        q.pop();

        if (now == target) {
            return cnt;
        }

        for (int i = 0; i &lt; words.size(); ++i) {
            if (visited[i]) continue;
            if (is1Diff(now, words[i])) {
                q.push({words[i], cnt + 1});
                visited[i] = true;
            }
        }
    }

    return 0;
}</code></pre>
<h2 id="🥜-채점bfs">🥜 채점(BFS)</h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/4f2e94da-4dd7-40f0-bf58-b8cdf2ba9c7c/image.png" /></p>