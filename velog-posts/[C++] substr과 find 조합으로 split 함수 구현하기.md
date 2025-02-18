<h2 id="split"><code>split()</code></h2>
<p><code>string</code>형 데이터를 어떤 기호를 기준으로 두고 잘라야 할 때가 있다.
<code>Python</code>, <code>Java</code>, <code>JavaScript</code> 모두 가지고 있는 함수인데 <code>c++</code>엔 없다.
<code>a.split(&quot;,&quot;);</code>와 같이 사용되는데 구현하는 방법은 여러가지다.
이 글에서는 아래 두 함수를 조합하여 구현해보자.</p>
<h2 id="substr"><code>substr()</code></h2>
<p><code>string</code>을 인덱스 기반으로 잘라주는 도구다.
인자 하나만 쓰면 해당 인자부터 끝까지 잘라주고,
인자가 두개면 첫 번째 인자부터 두 번째 인자 길이만큼 떼어준다.</p>
<p><code>str.substr(0)</code> = <code>str[0] ~ str[str.length()]</code>
<code>str.substr(3, 5)</code> = <code>str[3] ~ str[3+5-1]</code></p>
<h2 id="find"><code>find()</code></h2>
<p><code>string</code>에서 원하는 문자를 찾을 때 사용한다.
인자가 하나면 <code>string</code>에서 해당 문자가 처음 등장하는 인덱스를 뱉고
인자가 두개면 첫 번째 인자(문자)를 두 번째 인자(탐색 시작 인덱스)부터 탐색한다.
만약 찾는 문자가 없으면 <code>no position</code>이라는 의미의 <code>string::npos</code>를     뱉는다.</p>
<h2 id="split-구현하기"><code>split</code> 구현하기</h2>
<pre><code class="language-c++">#include &lt;iostream&gt;
#include &lt;string&gt;
#include &lt;vector&gt;
using namespace std;

int main() {
    string str;
    cin &gt;&gt; str; // 10-20+15+25-30

    vector&lt;string&gt; v;
    int prev = 0;
    int curr = str.find('-');
    while (curr != string::npos) {
        string tmp = str.substr(prev, curr - prev);
        v.push_back(tmp);
        prev = curr + 1;
        curr = str.find('-', prev);
    }
    v.push_back(str.substr(prev));

    for (int i = 0; i &lt; v.size(); i++) {
        cout &lt;&lt; v[i] &lt;&lt; &quot;\n&quot;;
    }
    /*
    10
    20+15+25
    30
    */
}</code></pre>
<h2 id="관련-문제">관련 문제</h2>
<p><a href="https://www.acmicpc.net/problem/1541">백준 1541. 잃어버린 괄호</a>
<a href="https://api.velog.io/rss/@coolgamja_">감자 풀이 보러가기</a></p>