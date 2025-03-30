<h3 id="level-2-null-처리하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59410">[Level 2] NULL 처리하기</a></h3>
<pre><code class="language-sql">SELECT ANIMAL_TYPE, COALESCE(NAME, 'No name'), SEX_UPON_INTAKE
FROM ANIMAL_INS</code></pre>
<h3 id="level-2-root-아이템-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/273710">[Level 2] ROOT 아이템 구하기</a></h3>
<pre><code class="language-sql">SELECT ITEM_ID, ITEM_NAME
FROM ITEM_INFO
WHERE ITEM_ID IN (
    SELECT ITEM_ID
    FROM ITEM_TREE
    WHERE PARENT_ITEM_ID IS NULL
)
ORDER BY ITEM_ID</code></pre>
<h3 id="level-3-업그레이드-할-수-없는-아이템-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/273712">[Level 3] 업그레이드 할 수 없는 아이템 구하기</a></h3>
<pre><code class="language-sql">SELECT ITEM_ID, ITEM_NAME, RARITY
FROM ITEM_INFO
WHERE ITEM_ID NOT IN (
    SELECT ITEM_ID
    FROM ITEM_TREE
    WHERE ITEM_ID IN (
        SELECT DISTINCT PARENT_ITEM_ID
        FROM ITEM_TREE
    )
)
ORDER BY ITEM_ID DESC</code></pre>