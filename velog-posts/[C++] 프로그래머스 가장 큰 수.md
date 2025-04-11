<h2 id="🌽-문제">🌽 <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42746">문제</a></h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/9456d59d-5c7c-46f0-aa72-527e071e84fd/image.png" /></p>
<h2 id="🥔-풀이">🥔 풀이</h2>
<p>비교연산자를 커스텀해야 하는 문제.
채점할 때 케이스 11에서 자꾸 실패가 뜨길래 질문방을 참고했다.
입력이 [0, 0, 0]인 경우 &quot;000&quot;이 아니라 &quot;0&quot;으로 처리해야 한다.</p>
<h2 id="🥬-코드">🥬 코드</h2>
<pre><code class="language-cpp">#include &lt;iostream&gt;
#include &lt;algorithm&gt;
#include &lt;string&gt;
#include &lt;vector&gt;

using namespace std;

bool cmp(string n, string m) {    
    string a = n + m;
    string b = m + n;
    return a &gt; b;
}

string solution(vector&lt;int&gt; numbers) {
    vector&lt;string&gt; nums;
    string answer = &quot;&quot;;
    for (int i = 0; i &lt; numbers.size(); i++) {
        nums.push_back(to_string(numbers[i]));
    }
    sort(nums.begin(), nums.end(), cmp);
    for (int i = 0; i &lt; nums.size(); i++) {
        answer += nums[i];
    }
    if (answer[0] == '0') answer = &quot;0&quot;;
    return answer;
}</code></pre>
<h2 id="🥜-채점">🥜 채점</h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/11deacc3-8eb4-4540-8bb1-4b38397561cb/image.png" /></p>