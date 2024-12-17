<p>백준은 프로그래머스와 다르게 <code>cin</code>과 <code>cout</code>으로 입출력을 처리한다.
시간 초과가 났을 때 아래 코드를 추가하면 통과되는 문제들이 여럿 있었다.</p>
<pre><code class="language-cpp">ios::sync_with_stdio(false);
cin.tie();
cout.tie();</code></pre>
<p>솔직히 아무 생각 없이 썼는데
이쯤 되니 슬쩍 궁금해져서 찾아봤다.</p>
<p>그런데 충격 사실
저 세 줄 중 첫 줄만 입출력 속도를 높이는 데 기여하고 있었다.</p>
<h2 id="iossync_with_stdiofalse"><code>ios::sync_with_stdio(false);</code></h2>
<h3 id="1-기능">1. 기능</h3>
<blockquote>
<p>C++의 iostream과 C 표준 I/O(stdio)를 동기화하는 기능을 해제한다.</p>
</blockquote>
<h3 id="2-자세히">2. 자세히</h3>
<p>기본적으로, iostream은 C의 stdio와 연결되어 있어 printf, scanf 등과 함께 사용할 때 동기화를 유지한다.
동기화를 해제하면 <strong>iostream이 독립적인 버퍼를 사용하게 되어 입출력 속도가 빨라진다.</strong></p>
<p>하지만 <code>scanf, printf, puts, getchar, putchar</code> 등 C의 입출력 함수와 혼용하면 버퍼가 분리되어 출력 순서가 꼬이거나 데이터 일관성이 깨질 수 있다.
따라서 <code>cin, cout</code>만 사용하는 경우에 동기화 해제를 통해 입출력 속도를 효과적으로 향상시킬 수 있다.</p>
<h2 id="cintienull"><code>cin.tie(NULL);</code></h2>
<h3 id="1-기능-1">1. 기능</h3>
<blockquote>
<p>cin과 cout의 연결을 끊는다.</p>
</blockquote>
<h3 id="2-자세히-1">2. 자세히</h3>
<p>기본적으로 cin과 cout은 연결되어 있어서,
원래는 cin을 호출하면 자동으로 cout의 버퍼가 비워진다.</p>
<p><code>tie(NULL)</code>은 이 동작을 끊어내어,
cin 호출 시 cout의 버퍼를 강제로 비우지 않도록 만든다.</p>
<p>입력과 출력을 독립시키므로 입력 속도를 높일 수 있지만,
출력 순서가 보장되지 않을 수 있기 때문에 순서를 직접 관리해야 한다.</p>
<h3 id="3-번외">3. 번외</h3>
<p><code>cin.tie()</code>는 cin과 cout이 연동되도록(..) 설정하는 코드고,
<code>cout.tie()</code>는 cout의 연결을 설정하는 코든데
연결된 다른 출력 스트림이 없어서
아무 의미 없이 자리만 차지하는 넘이었던 것;</p>
<h2 id="입출력-속도-높이기">입출력 속도 높이기</h2>
<p>정리하자면, 아래 코드가 백준에서 먹히는 정석 코드다.</p>
<pre><code class="language-cpp">#include &lt;iostream&gt;
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    return 0;
}</code></pre>
<p>다만, 
<strong>1. 입출력 순서 안 꼬이게 잘 관리하기
2. C의 입출력 함수와 혼용하지 않기</strong>
요 두 가지만 잘 기억하여 사용하도록 하자.</p>