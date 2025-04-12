<h2 id="🌽-문제">🌽 <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42747">문제</a></h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/a656ef92-d84a-41fe-b9d4-dbd791a6184b/image.png" /></p>
<h2 id="🥔-풀이">🥔 풀이</h2>
<p>처음에는 아래와 같은 조건문을 가지고 걸렀다가,
이렇게 하면 citations안의 요소가 아닌 숫자는 답이 될 수 없음을 깨달았다.</p>
<pre><code class="language-cpp">if (citations[i] &gt; n) continue;
if (citations[citations[i] - 1] == citations[i]) {
    answer = citations[i];
    break;
}</code></pre>
<p>내림차순 정렬된 <code>citations</code>를 돌며,
인용수가 해당 인덱스값보다 크다면 <code>h</code>값을 인덱스값으로 갱신하길 반복한다.</p>
<h2 id="🥬-코드">🥬 코드</h2>
<pre><code class="language-cpp">#include &lt;algorithm&gt;
#include &lt;string&gt;
#include &lt;vector&gt;

using namespace std;

int solution(vector&lt;int&gt; citations) {
    sort(citations.begin(), citations.end(), greater&lt;int&gt;());

    int n = citations.size();
    int answer = 0;
    for (int i = 0; i &lt; n; i++) {
        if (citations[i] &gt;= i + 1) {
            answer = i + 1;
        }
        else break;
    }

    return answer;
}</code></pre>
<h2 id="🥜-채점">🥜 채점</h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/ca85e967-46a0-4cd7-af8b-a16cb0624cc7/image.png" /></p>