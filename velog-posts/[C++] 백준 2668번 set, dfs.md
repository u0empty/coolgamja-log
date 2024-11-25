<p>알고리즘 실력 향상을 위하여 매일 골드 이상 문제를 최소 한 문제씩 풀기로 결심하였다. (feat. 잔디매니절)
거런데 살짝 쫄리고 배고프니까 골드5에 도전</p>
<h2 id="2668-숫자고르기">2668. 숫자고르기</h2>
<p>100 이하의 n개의 숫자가 주어지며 1부터 시작하는 인덱스의 집합과 해당 인덱스가 갖는 값의 집합이 일치하도록 만드는 인덱스를 뽑아 출력하는 문제이다.
최대한 많은 수의 인덱스를 뽑는 것이 조건이다.</p>
<h2 id="풀이">풀이</h2>
<p>문제를 보니 뭔가 타고 dfs 같군 하는 생각은 들었는데
역시 나의 조고만 뇌로는 감당하기 어려운 문제임을 감지
15분 정도 고민해보다가 바로 구글 켜서 해결해 나갔다.</p>
<p>주어진 배열의 모든 인덱스에 대해 dfs를 수행해 줄건데,
인덱스를 타고 타고 가다가
맨 처음에 시작한 숫자를 다시 만났을 때 되돌아오는지 확인하고,
되돌아온 게 맞다면 타고 온 경로를 추가 추가 해주는 식으로 진행된다.</p>
<p>요 때 경로를 넣어줄 컨테이너를 <code>set&lt;int&gt;</code>으로 만들어줄건데
중복을 허용하지 않고 정렬이 가능한 연관 컨테이너의 일종이다.
사용법이 <code>map</code>이랑 비슷한 것 같다고 느꼈다.</p>
<h2 id="set">set</h2>
<p><code>map</code>처럼 기본 오름차순 정렬이고,
내림차순이고 싶다면 <code>greater&lt;&gt;</code>를 붙여주자.</p>
<h3 id="선언-값-삽입">선언, 값 삽입</h3>
<pre><code class="language-cpp">#include &lt;set&gt;

set&lt;int&gt; s; // 내림차순은 set&lt;int, greater&lt;int&gt;&gt; s;
s.insert(값);</code></pre>
<h3 id="데이터-접근">데이터 접근</h3>
<pre><code class="language-cpp">for (auto it : s) {
    cout &lt;&lt; it &lt;&lt; &quot;\n&quot;;
}</code></pre>
<h3 id="멤버-함수-find">멤버 함수 find</h3>
<p>연관 컨테이너라면 무족권 멤바 find가 훨 빠르다.
무적권은 아닌가?</p>
<pre><code class="language-cpp">auto it = s.find(찾을값);
cout &lt;&lt; *it &lt;&lt; &quot;\n&quot;;</code></pre>
<h2 id="코드">코드</h2>
<pre><code class="language-cpp">#include &lt;iostream&gt;
#include &lt;set&gt;
#include &lt;cstring&gt;

using namespace std;

int n;
int arr[101];
bool visit[101];
bool flag;
set&lt;int&gt; ans;

void dfs(int start, int now) {
    if (visit[now]) {
        if (start == now) {
            ans.insert(now);
            flag = true;
        }
        return;
    }

    visit[now] = true;
    dfs(start, arr[now]);
    if (flag) ans.insert(now);
}

int main() {
    cin &gt;&gt; n;
    for (int i = 1; i &lt;= n; i++) {
        cin &gt;&gt; arr[i];
    }

    for (int i = 1; i &lt;= n; i++) {
        memset(visit, false, sizeof(visit));
        flag = false;
        dfs(i, i);
    }

    cout &lt;&lt; ans.size() &lt;&lt; &quot;\n&quot;;
    for (auto it : ans) {
        cout &lt;&lt; it &lt;&lt; &quot;\n&quot;;
    }
}</code></pre>