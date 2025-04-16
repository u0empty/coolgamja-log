<h2 id="🌽-문제">🌽 <a href="https://school.programmers.co.kr/learn/courses/30/lessons/49189">문제</a></h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/01b5156d-5eb1-4739-bec9-fcb96642543f/image.png" /></p>
<h2 id="🥔-풀이">🥔 풀이</h2>
<p>BFS 기본 수준 활용 문제이다.
냅다 DFS로 박았다가 빠꾸하고 마음의 평화를 찾았다.</p>
<p>DFS는 어떤 순서로든 방문할 수 있어 거리 계산을 일일이 관리해야 하고,
최단 거리인지 보장하기 어렵다.</p>
<p>BFS는 항상 레벨 순으로 탐색하는 최단 거리 탐색에 최적화된 알고리즘이다.
<code>가장 먼 노드 = 최단 거리 기준 가장 큰 값</code>을 구하는 것이므로 BFS로 풀어내자.</p>
<p>먼저, 엣지를 갖다가 양방향 그래프로 가공해준다.
1번 노드와의 거리를 저장하는 벡터를 생성하고 -1로 초기화한다.</p>
<p>고담에 BFS로 들어가자.
출발 노드인 1번 노드의 거리를 0으로 갱신하고,
차례로 탐색할 <code>queue</code>에 담아주면서 <code>while</code>문 입장.</p>
<p><code>queue</code> 앞머리를 현재 탐색 노드로 저장하고, <code>pop</code> 한다.
현재 탐색 노드에서 갈 수 있는 노드를 돌며 거리가 갱신된 적 없다면(<code>-1</code>)
<code>현재 노드 + 1</code>로 갱신하는 동시에 <code>queue</code>에 넣어주기를
<code>queue</code>가 비기 전까지 반복한다.</p>
<p>갱신된 <code>dist</code>의 최댓값을 찾고,
그 값과 같은 경우 <code>count</code>하여 <code>return</code>하면 끋</p>
<p><code>*max_element</code>랑 <code>count_if</code>는 첨 써봤는데 아주 편리하다.
간단한 사용법을 정리해보자.</p>
<h3 id="max_element-min_element">max_element (min_element)</h3>
<p><code>#include &lt;algorithm&gt;</code> 여기 들어있다.</p>
<ol>
<li><p><code>max_element(start, end)</code>
: 범위 내 최대값의 iterator 반환</p>
</li>
<li><p><code>*max_element(start, end)</code>
: 범위 내 최대값의 value 반환</p>
</li>
<li><p><code>min_element(start, end)</code>
: 범위 내 최소값의 iterator 반환</p>
</li>
<li><p><code>*min_element(start, end)</code>
: 범위 내 최소값의 value 반환</p>
</li>
</ol>
<h3 id="count_if-count">count_if (count)</h3>
<p>마찬가지로 <code>#include &lt;algorithm&gt;</code> 여기 들어있다.</p>
<ol>
<li><p><code>count(start, end, value)</code>
: 범위 내 value와 일치하는 값의 개수 반환</p>
</li>
<li><p><code>count_if(start, end, 조건(return bool))</code>
: 범위 내 조건에 맞는 값의 개수 반환</p>
</li>
</ol>
<p>이 때 조건문은 람다 함수 구조 <code>[]() {};</code>를 갖는다.</p>
<p><code>[]</code>: 람다 내부에서 외부 변수에 접근할지 여부를 명시한다.</p>
<ul>
<li><code>[]</code>    외부 변수 캡처하지 않음</li>
<li><code>[x]</code>    외부 변수 x를 값으로 복사</li>
<li><code>[&amp;x]</code>    외부 변수 x를 참조로 캡처</li>
<li><code>[=]</code>    외부 모든 변수를 값으로 복사</li>
<li><code>[&amp;]</code>    외부 모든 변수를 참조로 캡처</li>
<li><code>[=, &amp;x]</code>    기본은 값, x만 참조</li>
</ul>
<p><code>()</code>: 매개변수 리스트로, 함수처럼 인자를 받을 수 있다.</p>
<h2 id="🥬-코드">🥬 코드</h2>
<pre><code class="language-cpp">#include &lt;algorithm&gt;
#include &lt;vector&gt;
#include &lt;queue&gt;

using namespace std;

int solution(int n, vector&lt;vector&lt;int&gt;&gt; edge) {
    vector&lt;vector&lt;int&gt;&gt; graph(n + 1);
    vector&lt;int&gt; dist(n + 1, -1);
    queue&lt;int&gt; q;

    for (auto e : edge) {
        graph[e[0]].push_back(e[1]);
        graph[e[1]].push_back(e[0]);
    }

    q.push(1);
    dist[1] = 0;

    while (!q.empty()) {
        int curr = q.front();
        q.pop();

        for (int next : graph[curr]) {
            if (dist[next] == -1) {
                dist[next] = dist[curr] + 1;
                q.push(next);
            }
        }
    }

    int maxDist = *max_element(dist.begin(), dist.end());
    int cnt = count_if(dist.begin(), dist.end(), [maxDist](int d) {
        return d == maxDist;
    });

    return cnt;
}</code></pre>
<h2 id="🥜-채점">🥜 채점</h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/186f6167-41c3-4aef-81be-48bed6aa6ea4/image.png" /></p>