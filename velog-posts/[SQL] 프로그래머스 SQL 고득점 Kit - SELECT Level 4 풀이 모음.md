<h3 id="level-4-서울에-위치한-식당-목록-출력하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/131118">[Level 4] 서울에 위치한 식당 목록 출력하기</a></h3>
<pre><code class="language-sql">SELECT 
    I.REST_ID, 
    I.REST_NAME, 
    I.FOOD_TYPE, 
    I.FAVORITES, 
    I.ADDRESS, 
    ROUND(AVG(R.REVIEW_SCORE), 2) SCORE
FROM REST_INFO I
JOIN REST_REVIEW R
ON I.REST_ID = R.REST_ID
WHERE I.ADDRESS LIKE '서울%'
GROUP BY I.REST_ID, I.REST_NAME, I.FOOD_TYPE, I.FAVORITES, I.ADDRESS
ORDER BY SCORE DESC, I.FAVORITES DESC;</code></pre>
<h3 id="level-4-오프라인온라인-판매-데이터-통합하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/131537">[Level 4] 오프라인/온라인 판매 데이터 통합하기</a></h3>
<pre><code class="language-sql">SELECT DATE_FORMAT(SALES_DATE, '%Y-%m-%d') SALES_DATE, PRODUCT_ID, USER_ID, SALES_AMOUNT
FROM (
    SELECT SALES_DATE, PRODUCT_ID, USER_ID, SALES_AMOUNT
    FROM ONLINE_SALE
    WHERE YEAR(SALES_DATE) = 2022 AND MONTH(SALES_DATE) = 3

    UNION ALL

    SELECT SALES_DATE, PRODUCT_ID, NULL AS USER_ID, SALES_AMOUNT
    FROM OFFLINE_SALE
    WHERE YEAR(SALES_DATE) = 2022 AND MONTH(SALES_DATE) = 3
) DATA
ORDER BY SALES_DATE, PRODUCT_ID, USER_ID</code></pre>
<h3 id="level-4-특정-세대의-대장균-찾기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/301650">[Level 4] 특정 세대의 대장균 찾기</a></h3>
<pre><code class="language-sql">SELECT ID
FROM ECOLI_DATA
WHERE PARENT_ID IN (
    SELECT B.ID
    FROM ECOLI_DATA A
    JOIN ECOLI_DATA B
    ON A.ID = B.PARENT_ID
    WHERE A.PARENT_ID IS NULL
    ORDER BY B.ID
)</code></pre>