<h3 id="level-3-대장균들의-자식의-수-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/299305">[Level 3] 대장균들의 자식의 수 구하기</a></h3>
<pre><code class="language-sql">SELECT A.ID, COALESCE(COUNT(B.ID), 0) CHILD_COUNT
FROM ECOLI_DATA A
LEFT JOIN ECOLI_DATA B
ON A.ID = B.PARENT_ID
GROUP BY A.ID
ORDER BY A.ID</code></pre>
<h3 id="level-3-대장균의-크기에-따라-분류하기-1"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/299307">[Level 3] 대장균의 크기에 따라 분류하기 1</a></h3>
<pre><code class="language-sql">SELECT
    ID,
    CASE
        WHEN SIZE_OF_COLONY &lt;= 100 THEN 'LOW'
        WHEN SIZE_OF_COLONY BETWEEN 101 AND 1000 THEN 'MEDIUM'
        ELSE 'HIGH'
    END AS SIZE
FROM ECOLI_DATA 
ORDER BY ID</code></pre>
<h3 id="level-3-대장균의-크기에-따라-분류하기-2"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/301649">[Level 3] 대장균의 크기에 따라 분류하기 2</a></h3>
<pre><code class="language-sql">SELECT
    ID,
    CASE
        WHEN NTILE(4) OVER (ORDER BY SIZE_OF_COLONY DESC) = 1 THEN 'CRITICAL'
        WHEN NTILE(4) OVER (ORDER BY SIZE_OF_COLONY DESC) = 2 THEN 'HIGH'
        WHEN NTILE(4) OVER (ORDER BY SIZE_OF_COLONY DESC) = 3 THEN 'MEDIUM'
        ELSE 'LOW'
    END COLONY_NAME
FROM ECOLI_DATA
ORDER BY ID</code></pre>