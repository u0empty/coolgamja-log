<p>이진 탐색은 정렬되어 있는 배열을 반으로 쪼개 범위를 옮겨가며 탐색하는 방법이다.
시간복잡도는 N(log N)이며 C++의 STL에서 <code>binary_search</code>라는 함수를 제공한다.
찾으면 true를, 그렇지 못한 경우 false를 반환한다.
범위의 처음, 마지막, 그리고 찾을 값을 넘겨주면 된다.</p>
<h3 id="직접-구현">직접 구현</h3>
<pre><code class="language-cpp">vector&lt;int&gt; v(크기); // &lt;-- 오름차순 정렬된 벡터

bool binarySearch(int num) {
    int start = 0;
    int end = v.size() - 1;
    int mid;

    while(start &lt;= end) {
        mid = (start + end) / 2;

        if (v[mid] == num) return true;
        else if (v[mid] &lt; num) start = mid + 1;
        else end = mid - 1;
    }

    return false;
}</code></pre>
<p><a href="https://www.acmicpc.net/problem/10815">백준 10815번</a> 풀 때 썼는데 직접 구현보다 함수 쓴 게 훨 빠르다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/a7148c89-bb39-4697-8c8a-4b6885dd1698/image.png" /></p>
<h3 id="stl-binary_search-함수">STL binary_search 함수</h3>
<pre><code class="language-cpp">#include &lt;algorithm&gt;

vector&lt;int&gt; v(크기); // &lt;-- 오름차순 정렬된 벡터

if (binary_search(v.begin(), v.end(), 찾을 수)) {
    return 1;
}</code></pre>
<p>요 문제 풀 때 주의할 점은 벡터 오름차순 정렬이 필요하다는 것과 아래 코드를 꼭 넣어줘야 한다는 점.</p>
<pre><code class="language-c++">ios::sync_with_stdio(false);
cin.tie(0);
cout.tie(0);</code></pre>
<p>요새는 알아서 최적화 해줘서 필요없다 뭐 그런 말을 철썩 같이(사실은 쓰기 귀찮아서) 믿고 있던 나로서는 굉장한 배신이 아닐 수가 없다.
참나 ~</p>
<p><a href="https://www.acmicpc.net/problem/14425">14425번</a>도 같은 방법으로 잘 풀린다.</p>