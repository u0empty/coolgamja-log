<p>얼마 전 11650번을 풀 때 벡터를 두 개나 만들어서 굉장히 복잡하게 풀었다. 시간도 오래 걸리고 생긴 것도 못생겨서 맘에 안들었지만 맞았다는 사실에 의의를 두고 넘어간 문젠데 그 다음 단계 문제를 풀려고 보니까 저번처럼 그지같이 풀기가 너무 너무 싫은거다.</p>
<p>아유 하나 더 배울 때 됐다 하고 vector에 pair 넣어서 풀었는데 어우 아주 속이 시원해져서 잊어먹기 전에 머리에 꽂아두려고 갖고왔다.</p>
<h3 id="11650-좌표-정렬하기">11650. 좌표 정렬하기</h3>
<p>먼저 11650번 저번 그 똥코드</p>
<pre><code class="language-c++">#include &lt;iostream&gt;
#include &lt;algorithm&gt;
#include &lt;vector&gt;

using namespace std;

int n;
vector&lt;vector&lt;int&gt;&gt; posV(100001);
vector&lt;vector&lt;int&gt;&gt; negV(100001);

int main() {
    cin &gt;&gt; n;
    for (int i = 0; i &lt; n; i++) {
        int x, y;
        cin &gt;&gt; x &gt;&gt; y;
        if (x &lt; 0) negV[-x].push_back(y);
        else posV[x].push_back(y);
    }

    for (int i = 0; i &lt; 100001; i++) {
        sort(posV[i].begin(), posV[i].end());
    }
    for (int i = 0; i &lt; 100001; i++) {
        sort(negV[i].begin(), negV[i].end());
    }

    for (int i = 100000; i &gt; 0; i--) {
        if (negV[i].empty()) continue;
        for (int j = 0; j &lt; negV[i].size(); j++) {
            cout &lt;&lt; -i &lt;&lt; &quot; &quot; &lt;&lt; negV[i][j] &lt;&lt; &quot;\n&quot;;
        }
    }
    for (int i = 0; i &lt; 100001; i++) {
        if (posV[i].empty()) continue;
        for (int j = 0; j &lt; posV[i].size(); j++) {
            cout &lt;&lt; i &lt;&lt; &quot; &quot; &lt;&lt; posV[i][j] &lt;&lt; &quot;\n&quot;;
        }
    }

    return 0;
}</code></pre>
<p>아우 드러워</p>
<p>but 오늘 새로 짠 코드</p>
<pre><code class="language-c++">#include &lt;iostream&gt;
#include &lt;algorithm&gt;
#include &lt;vector&gt;

using namespace std;

int n, x, y;
vector&lt;pair&lt;int, int&gt;&gt; v;

int main() {
    cin &gt;&gt; n;
    for (int i = 0; i &lt; n; i++) {
        cin &gt;&gt; x &gt;&gt; y;
        v.push_back({ x, y });
    }

    sort(v.begin(), v.end());

    for (int i = 0; i &lt; n; i++) {
        cout &lt;&lt; v[i].first &lt;&lt; &quot; &quot; &lt;&lt; v[i].second &lt;&lt; &quot;\n&quot;;
    }

    return 0;
}</code></pre>
<p>이쁘다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/44cb99fb-a602-4212-ae1e-8e9fb6117094/image.png" /></p>
<p>빠르다.</p>
<h3 id="11651-좌표-정렬하기-2">11651. 좌표 정렬하기 2</h3>
<p>11651번은 y 기준이라 cmp 함수만 추가해주면 된다.</p>
<pre><code class="language-c++">#include &lt;iostream&gt;
#include &lt;algorithm&gt;
#include &lt;vector&gt;

using namespace std;

vector&lt;pair&lt;int, int&gt;&gt; v;

int n;

bool cmp(pair&lt;int, int&gt; a, pair&lt;int, int&gt; b) {
    if (a.second == b.second) {
        return a.first &lt; b.first;
    }
    else {
        return a.second &lt; b.second;
    }
}

int main() {
    cin &gt;&gt; n;
    for (int i = 0; i &lt; n; i++) {
        int x, y;
        cin &gt;&gt; x &gt;&gt; y;
        v.push_back({ x, y });
    }

    sort(v.begin(), v.end(), cmp);

    for (int i = 0; i &lt; n; i++) {
        cout &lt;&lt; v[i].first &lt;&lt; &quot; &quot; &lt;&lt; v[i].second &lt;&lt; &quot;\n&quot;;
    }

    return 0;
}</code></pre>
<p>자료구조가 이러게 중요한 줄 알았으면 씨쁠 안맞았지
아니지 알았는데 그냥 모단거지 바보
언젠간 한 번 삭 훑어야쓰것다..</p>