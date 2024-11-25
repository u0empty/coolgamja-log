<p>다음에 까먹을 게 분명해서 적어본다.</p>
<h2 id="char-to-int">char to int</h2>
<p><a href="https://www.acmicpc.net/problem/1427">백준 1427. 소트인사이드</a></p>
<p>기다란 수를 string으로 받아서 하나씩 찢은 뒤 정렬해야 할 때 유용하다.</p>
<pre><code class="language-c++">#include &lt;iostream&gt;
#include &lt;string&gt;

using namespace std;

int main() {
    string n;
    cin &gt;&gt; n;

    for (int i = 0; i &lt; n.size(); i++) {
        int num = n[i] - '0';
    }

    return 0;
}</code></pre>
<p><code>- '0'</code> 말고 <code>* 1</code> 해봤는데 '2'가 50이 되는 magic</p>
<h2 id="메모리-초과">메모리 초과</h2>
<p><a href="https://www.acmicpc.net/problem/10989">백준 10989. 수 정렬하기 3</a></p>
<p>int는 4바이트다. 그런데 받아야 할 수의 개수가 10,000,000개라면 40MB가 되어 대부분의 알고리즘 제한 용량에 걸리게 된다. 그런데 이 때 받아야 할 수가 10,000을 넘지 않고 중복도 허용한다면 아래 방법을 사용할 수 있다.</p>
<p>모든 수를 죄다 받아서 곧이곧대로 정렬하는 게 아니라, 수가 몇번이나 나왔는지 그 개수를 기록하는 배열을 이용할 수 있다.</p>
<pre><code class="language-c++">#include &lt;iostream&gt;

using namespace std;

int cnt[10001] = { 0, };

int main() {
    int n;
    cin &gt;&gt; n;

    for (int i = 0; i &lt; n; i++) {
        int num;
        cin &gt;&gt; num;
        cnt[num]++;
    }

    for (int i = 0; i &lt; 10001; i++) {
        for (int j = 0; j &lt; cnt[i]; j++) {
            cout &lt;&lt; i &lt;&lt; &quot;\n&quot;;
        }
    }

    return 0;
}</code></pre>
<p>출력 부분의 for문은 num을 vector에 넣어두면 vector.size() 까지로 그 범위를 최대한 줄일 수 있다.</p>
<pre><code class="language-c++">ios_base::sync_with_studio(false);
cin.tie(NULL);
cout.tie(NULL);</code></pre>
<p>요거는 입출력 속도 최적화 코드.
없어도 통과는 되는데 언제 사용할 지 모르니 일단 적어두기.
메모장이냐</p>
<h2 id="sort-내림차순">sort 내림차순</h2>
<p><a href="https://www.acmicpc.net/problem/1427">백준 1427. 소트인사이드</a></p>
<p>sort는 기본적으로 오름차순을 지원한다.
내림차순은 comp 함수같은 걸로도 구현할 수 있지만, 더 간단한 방법이 있다.</p>
<pre><code class="language-c++">#include &lt;iostream&gt;
#include &lt;algorithm&gt;

using namespace std;

int main() {
    int num[1001]; // 이미 갖고있다 치자
    sort(num, num + 1001, greater&lt;&gt;());

    return 0;
}</code></pre>
<p>less&lt;&gt;()는 오름차순과 같아 굳이 넣을 필욘 없고,
comp 함수는 아래와 같이 구현할 수 있다.</p>
<pre><code class="language-c++">bool comp(int a, int b) {
    return a &gt; b;
}

sort(num, num + n, comp);</code></pre>
<h2 id="2차원-값을-인덱스로-받을-때">2차원 값을 인덱스로 받을 때</h2>
<p><a href="https://www.acmicpc.net/problem/11650">백준 11650. 좌표 정렬하기</a></p>
<p>-10,000 부터 10,000 값을 가질 수 있는 좌표 값을 입력받아 x가 작은순으로, x가 같으면 y가 작은순으로 정렬해야 한다.</p>
<p>벡터의 인덱스값을 x로, v[x]에 push_back할 값을 y로 두고 풀었는데 자꾸 틀리길래 카만히 생각해보니 음수 index는 존재하지 않는 걸 깨달음. 웁스</p>
<p>두 가지 방법을 쓸 수 있는데</p>
<ul>
<li>크기를 두 배로 놓고 <code>v[인덱스 + 크기].push_back()</code> 하는 방법</li>
<li>음수 vector와 양수 vector를 각각 받고 이 때 음수는 v[-x]에 저장하는 방법</li>
</ul>
<p>뭔가 객체를 하나 더 만들기 싫어서 첫 번째 방법을 썼다가 오히려 헷갈려서 그냥 두 번째 방법을 사용했다.</p>