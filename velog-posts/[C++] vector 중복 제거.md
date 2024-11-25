<h2 id="백준-1181-단어-정렬">백준 1181. 단어 정렬</h2>
<p>N(1 ~ 20,000)개의 문자열(50자 이하)을</p>
<ol>
<li>길이가 짧은 순</li>
<li>사전순
으로 정렬하되 중복 단어는 하나만 남겨 출력하는 문제이다.</li>
</ol>
<h2 id="풀이">풀이</h2>
<p>sort와 unique를 사용하기 위해 algorithm 라이브러리를 include 하자.
unique는 연속된 중복 요소를 뒤로 넘겨주어 erase와 함께 중복 제거에 사용된다.
근데 unique의 반환값이 뭔지를 모르겠다.
인덱슨가 싶어 int에도 담아보고
중복되는 첫번째 값인가 싶어 string에도 담아봤는데 안담긴다.
주소값인가? 모르것다.</p>
<p>cmp 함수에 길이가 같은 경우도 고려해주는 것이 포인트다.
요거 없을 때도 예제 입력은 잘 출력됐는데 틀렸다고 뜨는 걸 보니 내가 생각지 못한 다른 뭔가가 있는거겠지</p>
<p>중복 단어가 제거되어 n보다 같거나 작아졌을테니
출력 시 벡터의 크기만큼 반복 출력해주면 완성시 ~</p>
<h2 id="코드">코드</h2>
<pre><code class="language-cpp">#include &lt;iostream&gt;
#include &lt;algorithm&gt;
#include &lt;vector&gt;

using namespace std;

int n;
vector&lt;string&gt; v;

bool cmp(string a, string b) {
    if (a.length() == b.length()) {
        return a &lt; b;
    }
    else {
        return a.length() &lt; b.length();
    }
}

int main() {
    cin &gt;&gt; n;
    for (int i = 0; i &lt; n; ++i) {
        string s;
        cin &gt;&gt; s;
        v.push_back(s);
    }
    sort(v.begin(), v.end(), cmp);
    v.erase(unique(v.begin(), v.end()), v.end());

    for (int i = 0; i &lt; v.size(); i++) {
        cout &lt;&lt; v[i] &lt;&lt; &quot;\n&quot;;
    }

    return 0;
}</code></pre>