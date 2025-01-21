<p><img alt="" src="https://velog.velcdn.com/images/coolgamja_/post/307cb595-250b-4147-bf74-e582693b3bb8/image.png" /></p>
<h2 id="기존-코드">기존 코드</h2>
<h3 id="1-상태관리-핸들러">1. 상태관리, 핸들러</h3>
<pre><code class="language-typescript">  const [isSearching, setIsSearching] = useState(false);
  const [isPicking, setIsPicking] = useState(false);
  const [isAdding, setIsAdding] = useState(false);
  const [isEditing, setIsEditing] = useState(false);
  const [isDeleting, setIsDeleting] = useState(false);

  const handleSearchFieldOpen = () =&gt; setIsSearching(true);
  const handleSearchFieldClose = () =&gt; setIsSearching(false);

  const handleTimePickerOpen = () =&gt; setIsPicking(true);
  const handleTimePickerClose = () =&gt; setIsPicking(false);

  const handleAddRecordOpen = () =&gt; setIsAdding(true);
  const handleAddRecordClose = () =&gt; setIsAdding(false);

  const handleEditRecordOpen = () =&gt; setIsEditing(true);
  const handleEditRecordClose = () =&gt; setIsEditing(false);

  const handleDeleteRecordOpen = () =&gt; setIsDeleting(true);
  const handleDeleteRecordClose = () =&gt; setIsDeleting(false);</code></pre>
<h3 id="2-사용-예시">2. 사용 예시</h3>
<pre><code>&lt;popup onClose={handleEditRecordClose} /&gt;</code></pre><h2 id="모여라">모여라</h2>
<h3 id="상태관리-핸들러">상태관리, 핸들러</h3>
<pre><code class="language-typescript">  const [state, setState] = useState({
    isSearching: false,
    isPicking: false,
    isAdding: false,
    isEditing: false,
    isDeleting: false,
  });

  const openState = (key: string) =&gt;
    setState((prev) =&gt; ({ ...prev, [key]: true }));
  const closeState = (key: any) =&gt;
    setState((prev) =&gt; ({ ...prev, [key]: false }));</code></pre>
<h3 id="사용-예시">사용 예시</h3>
<pre><code>&lt;popup onClose={() =&gt; closeState('isEditing')} /&gt;</code></pre><h2 id="그른데">그른데</h2>
<p>정리하고보니
핸들러를 건너뛴 그냥..
한 곳에 모으기만 한 코드 같다</p>