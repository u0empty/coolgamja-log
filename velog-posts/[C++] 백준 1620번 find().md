<p>어떤 문제를 풀기 위해서 새롭게 배우는 개념들에 대해,
그 문제를 풀 수 있을 만큼만 알고 있어서 문제라고 생각했는데
계속 풀면서 계속 새로 배우면 되지 싶다 ~</p>
<h2 id="1620-나는야-포켓몬-마스터-이다솜">1620. 나는야 포켓몬 마스터 이다솜</h2>
<p>n개의 포켓몬 도감이 주어지고 m개의 숫자 혹은 문자로 된 문제가 주어진다.
문제가 숫자이면 도감의 숫자 번째 포켓몬을 출력하고
문제가 문자이면 도감에서 해당 포켓몬이 몇 번째인지 출력한다.</p>
<h2 id="풀이">풀이</h2>
<p>처음에는 <code>vector&lt;string&gt; v</code>에 담아서 숫자면 <code>v[숫자-1]</code>,
문자면 <code>find(v.begin(), v.end(), 문자)</code> 해서 풀었는데
find를 못찾는다는 컴파일 에러가 뜨는 거다.</p>
<p>알고 보니까 <code>find</code>를 쓰려면 <code>algorithm</code>을 include 해줘야 하는데
visual studio code에서 에러가 나지 않았던 이유는
다른 헤더가 <code>algorithm</code>을 포함하고 있었을 수도 있다는 걸 알았다.
싱기</p>
<p>헤더에 포함해주고 다시 냈는데 이번엔 시간 초과가 난다.
그러면 정렬을 하고 binary_search를 써야것군 생각했는데
binary search는 값의 유무만 알 수 있다.</p>
<p>그러면 index 값과 name을 vector 말고 <code>map</code>에 넣어두고 찾으면 쓰겄다.
again 시간 초과
ㅇㄴ</p>
<p>map의 key로 value를 찾는 건 금방인데 value로 key를 찾을 때가 문젠가 싶어
문제가 숫자인 경우는 <code>vector&lt;string&gt;</code>에서 찾고,
문자인 경우를 만들어둔 map에서 찾도록 수정했다.</p>
<p>해결 ~</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/92486c39-fda1-4f01-bbf7-e6dcd13ecaf8/image.png" /></p>
<h2 id="코드">코드</h2>
<pre><code class="language-c++">#include &lt;iostream&gt;
#include &lt;vector&gt;
#include &lt;string&gt;
#include &lt;map&gt;

using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);

    int n, m;
    cin &gt;&gt; n &gt;&gt; m;

    map&lt;string, int&gt; pom;
    vector&lt;string&gt; pov;
    string str;
    for (int i = 1; i &lt;= n; i++) {
        cin &gt;&gt; str;
        pom[str] = i;
        pov.push_back(str);
    }

    for (int i = 0; i &lt; m; i++) {
        cin &gt;&gt; str;
        if (isdigit(str[0])) {
            cout &lt;&lt; pov[stoi(str) - 1] &lt;&lt; &quot;\n&quot;;
        }
        else {
            cout &lt;&lt; pom.find(str)-&gt;second &lt;&lt; &quot;\n&quot;;
        }
    }

    return 0;
}</code></pre>
<h2 id="find">find()</h2>
<p><code>vector</code>랑 <code>map</code>을 같이 쓰면서 헷갈렸던 부분이 <code>find</code>이다.
<code>m.find(찾는값)</code>도 쓰고 <code>find(v.begin(), v.end(), 찾는값)</code>도 쓴다.
언제 어떤 자료구조에 사용할 수 있는지 간단히 정리해보자.</p>
<h3 id="find찾는값">?.find(찾는값)</h3>
<ol>
<li>사용 가능한 자료구조</li>
</ol>
<ul>
<li>주로 <strong>연관 컨테이너(associative containers)</strong> 에서 사용된다.</li>
<li>ex) map, set, unordered_map, unordered_set, string</li>
</ul>
<ol start="2">
<li>동작</li>
</ol>
<ul>
<li>컨테이너 내부에 특정 키 또는 값이 존재하는지 찾는다.</li>
<li>연관 컨테이너에서는 키에 대한 탐색이 빠르다(로그 또는 상수 시간).</li>
</ul>
<ol start="3">
<li>반환값</li>
</ol>
<ul>
<li>연관 컨테이너: 있으면 <code>iterator</code>, 없으면 <code>?.end()</code>.</li>
<li>문자열: 있으면 인덱스, 없으면 <code>std::string::npos</code>.</li>
</ul>
<h3 id="findbegin-end-찾는값">find(?.begin(), ?.end(), 찾는값)</h3>
<ol>
<li>사용 가능한 자료구조</li>
</ol>
<ul>
<li>모든 <strong>순차 컨테이너(sequence containers)</strong> 에서 사용할 수 있다.</li>
<li>연관 컨테이너에서도 사용 가능하지만, 비효율적이다.</li>
<li>ex) vector, deque, list, array 등</li>
</ul>
<ol start="2">
<li>동작</li>
</ol>
<ul>
<li>선형 탐색으로 첫 번째로 일치하는 요소를 찾는다.</li>
<li>시간 복잡도: O(n)</li>
</ul>
<ol start="3">
<li>반환값</li>
</ol>
<ul>
<li>있으면 <code>iterator</code>, 없으면 <code>?.end()</code>.</li>
</ul>