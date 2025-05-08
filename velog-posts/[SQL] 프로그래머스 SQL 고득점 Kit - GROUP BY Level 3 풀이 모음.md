<h3 id="level-3-대여-횟수가-많은-자동차들의-월별-대여-횟수-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/151139">[Level 3] 대여 횟수가 많은 자동차들의 월별 대여 횟수 구하기</a></h3>
<pre><code class="language-sql">SELECT
    MONTH(START_DATE) MONTH,
    CAR_ID,
    COUNT(*) RECORDS
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE
    START_DATE BETWEEN '2022-08-01' AND '2022-10-31'
    AND CAR_ID IN (
        SELECT CAR_ID
        FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
        WHERE START_DATE BETWEEN '2022-08-01' AND '2022-10-31'
        GROUP BY CAR_ID
        HAVING COUNT(*) &gt;= 5
    )
GROUP BY MONTH, CAR_ID
ORDER BY MONTH, CAR_ID DESC</code></pre>
<h3 id="level-3-자동차-대여-기록에서-대여중--대여-가능-여부-구분하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/157340">[Level 3] 자동차 대여 기록에서 대여중 / 대여 가능 여부 구분하기</a></h3>
<pre><code class="language-sql">SELECT
    CAR_ID,
    CASE 
        WHEN CAR_ID IN (
            SELECT CAR_ID
            FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
            WHERE START_DATE &lt;= '2022-10-16' AND END_DATE &gt;= '2022-10-16'
        )
        THEN '대여중'
        ELSE '대여 가능'
    END AS AVAILABILITY
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
GROUP BY CAR_ID
ORDER BY CAR_ID DESC;</code></pre>
<h3 id="level-3-즐겨찾기가-가장-많은-식당-정보-출력하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/131123">[Level 3] 즐겨찾기가 가장 많은 식당 정보 출력하기</a></h3>
<pre><code class="language-sql">SELECT FOOD_TYPE, REST_ID, REST_NAME, FAVORITES
FROM REST_INFO
WHERE (FOOD_TYPE, FAVORITES) IN (
    SELECT FOOD_TYPE, MAX(FAVORITES)
    FROM REST_INFO
    GROUP BY FOOD_TYPE
)
ORDER BY FOOD_TYPE DESC</code></pre>
<h3 id="level-3-조건에-맞는-사용자와-총-거래금액-조회하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/164668">[Level 3] 조건에 맞는 사용자와 총 거래금액 조회하기</a></h3>
<pre><code class="language-sql">SELECT U.USER_ID, U.NICKNAME, SUM(B.PRICE) TOTAL_SALES
FROM USED_GOODS_BOARD B
JOIN USED_GOODS_USER U
ON B.WRITER_ID = U.USER_ID
WHERE STATUS = 'DONE'
GROUP BY U.USER_ID
HAVING TOTAL_SALES &gt;= 700000
ORDER BY TOTAL_SALES</code></pre>
<h3 id="level-3-카테고리-별-도서-판매량-집계하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/144855">[Level 3] 카테고리 별 도서 판매량 집계하기</a></h3>
<pre><code class="language-sql">SELECT B.CATEGORY, SUM(S.SALES) TOTAL_SALES
FROM BOOK B
JOIN BOOK_SALES S
ON B.BOOK_ID = S.BOOK_ID
WHERE S.SALES_DATE BETWEEN '2022-01-01' AND '2022-01-31'
GROUP BY B.CATEGORY
ORDER BY B.CATEGORY</code></pre>
<h3 id="level-3-부서별-평균-연봉-조회하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/284529">[Level 3] 부서별 평균 연봉 조회하기</a></h3>
<pre><code class="language-sql">SELECT D.DEPT_ID, D.DEPT_NAME_EN, ROUND(AVG(E.SAL), 0) AVG_SAL
FROM HR_EMPLOYEES E
JOIN HR_DEPARTMENT D
ON E.DEPT_ID = D.DEPT_ID
GROUP BY DEPT_ID
ORDER BY AVG_SAL DESC</code></pre>
<h3 id="level-3-특정-조건을-만족하는-물고기별-수와-최대-길이-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/298519">[Level 3] 특정 조건을 만족하는 물고기별 수와 최대 길이 구하기</a></h3>
<pre><code class="language-sql">SELECT COUNT(ID) FISH_COUNT, MAX(LENGTH) MAX_LENGTH, FISH_TYPE
FROM FISH_INFO
GROUP BY FISH_TYPE
HAVING AVG(IFNULL(LENGTH, 10)) &gt; 33
ORDER BY FISH_TYPE</code></pre>