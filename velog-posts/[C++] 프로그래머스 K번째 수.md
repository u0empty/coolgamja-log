<h2 id="🌽-문제">🌽 <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42748">문제</a></h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/548c4e3e-4104-4c09-97f8-afd6cbaf6db2/image.png" /></p>
<h2 id="🥔-풀이">🥔 풀이</h2>
<p>아마도 벨로그에는 처음 올리는 것 같은 (SQL 제외) 프로그래머스 알고리즘 문제.
<code>cout</code>으로 디버깅이 된다는 사실을 오늘에야 알았다..
모르겠으면 좀 찾아보지는 다른 사람이 알려줘서 안 것도 참 감잔거 티내냐,,
오늘이라도 알아서 다행이다.</p>
<p>문제에 제시된 대로,
인덱스 값에 유의하여 배열을 자르고 정렬한 뒤 k번째 값을 <code>push</code>한다.</p>
<h2 id="🥬-코드">🥬 코드</h2>
<pre><code class="language-cpp">#include &lt;string&gt;
#include &lt;vector&gt;
#include &lt;algorithm&gt;

using namespace std;

vector&lt;int&gt; solution(vector&lt;int&gt; array, vector&lt;vector&lt;int&gt;&gt; commands) {
    vector&lt;int&gt; answer, v;

    for (int i = 0; i &lt; commands.size(); i++) {
        int a = commands[i][0];
        int b = commands[i][1];
        int c = commands[i][2];

        for (int k = a - 1; k &lt; b; k++) {
            v.push_back(array[k]);
        }

        sort(v.begin(), v.end());
        answer.push_back(v[c - 1]);
        v.clear();
    }

    return answer;
}</code></pre>
<h2 id="🥜-채점">🥜 채점</h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/e536b804-7f75-492a-964a-7005c80f9be1/image.png" /></p>