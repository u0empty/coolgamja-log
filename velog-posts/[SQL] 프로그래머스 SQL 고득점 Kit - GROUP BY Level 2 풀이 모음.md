<h3 id="level-2-자동차-종류-별-특정-옵션이-포함된-자동차-수-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/151137">[Level 2] 자동차 종류 별 특정 옵션이 포함된 자동차 수 구하기</a></h3>
<pre><code class="language-sql">SELECT CAR_TYPE, COUNT(CAR_ID) CARS
FROM CAR_RENTAL_COMPANY_CAR
WHERE
    OPTIONS LIKE '%통풍시트%'
    OR OPTIONS LIKE '%열선시트%'
    OR OPTIONS LIKE '%가죽시트%'
GROUP BY CAR_TYPE
ORDER BY CAR_TYPE</code></pre>
<h3 id="level-2-진료과별-총-예약-횟수-출력하기">[<a href="https://school.programmers.co.kr/learn/courses/30/lessons/132202">Level 2 진료과별 총 예약 횟수 출력하기</a></h3>
<pre><code class="language-sql">SELECT MCDP_CD 진료과코드, COUNT(PT_NO) 5월예약건수
FROM APPOINTMENT
WHERE APNT_YMD LIKE '2022-05%'
GROUP BY MCDP_CD
ORDER BY 5월예약건수, MCDP_CD</code></pre>
<h3 id="level-2-성분으로-구분한-아이스크림-총-주문량">[<a href="https://school.programmers.co.kr/learn/courses/30/lessons/133026">Level 2 성분으로 구분한 아이스크림 총 주문량</a></h3>
<pre><code class="language-sql">SELECT I.INGREDIENT_TYPE, SUM(F.TOTAL_ORDER) TOTAL_ORDER
FROM ICECREAM_INFO I
JOIN FIRST_HALF F
ON I.FLAVOR = F.FLAVOR
GROUP BY I.INGREDIENT_TYPE
ORDER BY TOTAL_ORDER</code></pre>
<h3 id="level-2-고양이와-개는-몇-마리-있을까"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59040">[Level 2] 고양이와 개는 몇 마리 있을까</a></h3>
<pre><code class="language-sql">SELECT ANIMAL_TYPE, COUNT(ANIMAL_ID) count
FROM ANIMAL_INS
WHERE ANIMAL_TYPE IN ('Cat', 'Dog')
GROUP BY ANIMAL_TYPE
ORDER BY ANIMAL_TYPE</code></pre>
<h3 id="level-2-동명-동물-수-찾기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59041">[Level 2] 동명 동물 수 찾기</a></h3>
<pre><code class="language-sql">SELECT NAME, COUNT(NAME) COUNT
FROM ANIMAL_INS
GROUP BY NAME
HAVING COUNT &gt;= 2
ORDER BY NAME</code></pre>
<h3 id="level-2-입양-시각-구하기1"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59412">[Level 2] 입양 시각 구하기(1)</a></h3>
<pre><code class="language-sql">SELECT HOUR(DATETIME) HOUR, COUNT(ANIMAL_ID) COUNT
FROM ANIMAL_OUTS
GROUP BY HOUR
HAVING HOUR BETWEEN 9 AND 19
ORDER BY HOUR</code></pre>
<h3 id="level-2-입양-시각-구하기2"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59413">[Level 2] 입양 시각 구하기(2)</a></h3>
<pre><code class="language-sql">WITH RECURSIVE TMP AS (
    SELECT 0 HOUR
    UNION ALL
    SELECT HOUR + 1
    FROM TMP
    WHERE HOUR &lt; 23
)
SELECT T.HOUR, COUNT(A.ANIMAL_ID) COUNT
FROM TMP T
LEFT JOIN ANIMAL_OUTS A
ON T.HOUR = HOUR(A.DATETIME) 
GROUP BY T.HOUR
ORDER BY T.HOUR</code></pre>
<h3 id="level-2-가격대-별-상품-개수-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/131530">[Level 2] 가격대 별 상품 개수 구하기</a></h3>
<pre><code class="language-sql">SELECT (PRICE DIV 10000) * 10000 PRICE_GROUP, COUNT(PRODUCT_ID) PRODUCTS
FROM PRODUCT
GROUP BY PRICE_GROUP
ORDER BY PRICE_GROUP</code></pre>
<h3 id="level-2-조건에-맞는-사원-정보-조회하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/284527">[Level 2] 조건에 맞는 사원 정보 조회하기</a></h3>
<pre><code class="language-sql">SELECT
    SUM(G.SCORE) SCORE,
    E.EMP_NO,
    E.EMP_NAME,
    E.POSITION,
    E.EMAIL
FROM HR_EMPLOYEES E
JOIN HR_GRADE G
ON E.EMP_NO = G.EMP_NO
GROUP BY E.EMP_NO, E.EMP_NAME, E.POSITION, E.EMAIL
ORDER BY SCORE DESC
LIMIT 1</code></pre>
<h3 id="level-2-노선별-평균-역-사이-거리-조회하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/284531">[Level 2] 노선별 평균 역 사이 거리 조회하기</a></h3>
<pre><code class="language-sql">SELECT
    ROUTE,
    CONCAT(ROUND(SUM(D_BETWEEN_DIST), 1), 'km') TOTAL_DISTANCE,
    CONCAT(ROUND(AVG(D_BETWEEN_DIST), 2), 'km') AVERAGE_DISTANCE
FROM SUBWAY_DISTANCE
GROUP BY ROUTE
ORDER BY SUM(D_BETWEEN_DIST) DESC</code></pre>
<h3 id="level-2-물고기-종류-별-잡은-수-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/293257">[Level 2] 물고기 종류 별 잡은 수 구하기</a></h3>
<pre><code class="language-sql">SELECT COUNT(I.FISH_TYPE) FISH_COUNT, N.FISH_NAME
FROM FISH_INFO I
LEFT JOIN FISH_NAME_INFO N
ON I.FISH_TYPE = N.FISH_TYPE
GROUP BY N.FISH_NAME
ORDER BY FISH_COUNT DESC</code></pre>
<h3 id="level-2-월별-잡은-물고기-수-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/293260">[Level 2] 월별 잡은 물고기 수 구하기</a></h3>
<pre><code class="language-sql">SELECT COUNT(ID) FISH_COUNT, MONTH(TIME) MONTH
FROM FISH_INFO
GROUP BY MONTH
ORDER BY MONTH</code></pre>