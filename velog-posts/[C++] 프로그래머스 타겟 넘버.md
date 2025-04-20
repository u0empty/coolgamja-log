<h2 id="🌽-문제">🌽 <a href="https://school.programmers.co.kr/learn/courses/30/lessons/43165">문제</a></h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/9e6fcedb-628d-4d2f-9659-2ccac53331e2/image.png" /></p>
<h2 id="🥔-풀이">🥔 풀이</h2>
<p>모든 경우의 수를 탐색해야 하므로 DFS로 풀어야 하는 문제.
nums의 모든 수를 다 사용하면: <code>lev == nums.size()</code>
누적합 sum이 target과 같은지 확인하여
경우의 수를 갱신하고 dfs 함수를 빠져나가길 반복한다.</p>
<h2 id="🥬-코드">🥬 코드</h2>
<pre><code class="language-cpp">#include &lt;vector&gt;

using namespace std;

int answer = 0;

void dfs(vector&lt;int&gt; nums, int t, int lev, int sum) {
    if (lev == nums.size()) {
        if (sum == t) answer++;
        return;
    }
    dfs(nums, t, lev + 1, sum + nums[lev]);
    dfs(nums, t, lev + 1, sum - nums[lev]);
}

int solution(vector&lt;int&gt; numbers, int target) {
    dfs(numbers, target, 0, 0);
    return answer;
}</code></pre>
<h2 id="🥜-채점">🥜 채점</h2>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/90184617-32ad-4a29-968c-04b51959ddf7/image.png" /></p>