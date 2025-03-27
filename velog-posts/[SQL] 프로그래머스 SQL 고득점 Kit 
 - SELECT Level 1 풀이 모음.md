<h3 id="level-1-흉부외과-또는-일반외과-의사-목록-출력하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/132203">[Level 1] 흉부외과 또는 일반외과 의사 목록 출력하기</a></h3>
<pre><code class="language-sql">SELECT DR_NAME, DR_ID, MCDP_CD, DATE_FORMAT(HIRE_YMD, &quot;%Y-%m-%d&quot;) AS HIRE_YMD
FROM DOCTOR
WHERE MCDP_CD = &quot;CS&quot; OR MCDP_CD = &quot;GS&quot;
ORDER BY HIRE_YMD DESC, DR_NAME</code></pre>
<h3 id="level-1-과일로-만든-아이스크림-고르기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/133025">[Level 1] 과일로 만든 아이스크림 고르기</a></h3>
<pre><code class="language-sql">SELECT I.FLAVOR
FROM ICECREAM_INFO AS I
JOIN FIRST_HALF AS F
ON I.FLAVOR = F.FLAVOR
WHERE F.TOTAL_ORDER &gt; 3000 AND I.INGREDIENT_TYPE = 'fruit_based'
ORDER BY F.TOTAL_ORDER DESC</code></pre>
<h3 id="level-1-평균-일일-대여-요금-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/151136">[Level 1] 평균 일일 대여 요금 구하기</a></h3>
<pre><code class="language-sql">SELECT ROUND(AVG(DAILY_FEE), 0) AS AVERAGE_FEE
FROM CAR_RENTAL_COMPANY_CAR
WHERE CAR_TYPE = 'SUV'</code></pre>
<h3 id="level-1-강원도에-위치한-생산공장-목록-출력하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/131112">[Level 1] 강원도에 위치한 생산공장 목록 출력하기</a></h3>
<pre><code class="language-sql">SELECT FACTORY_ID, FACTORY_NAME, ADDRESS
FROM FOOD_FACTORY
WHERE ADDRESS LIKE '강원도%'
ORDER BY FACTORY_ID</code></pre>
<h3 id="level-1-인기있는-아이스크림"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/133024">[Level 1] 인기있는 아이스크림</a></h3>
<pre><code class="language-sql">SELECT FLAVOR
FROM FIRST_HALF
ORDER BY TOTAL_ORDER DESC, SHIPMENT_ID</code></pre>
<h3 id="level-1-12세-이하인-여자-환자-목록-출력하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/132201">[Level 1] 12세 이하인 여자 환자 목록 출력하기</a></h3>
<pre><code class="language-sql">SELECT PT_NAME, PT_NO, GEND_CD, AGE, COALESCE(TLNO, 'NONE') AS TLNO
FROM PATIENT
WHERE AGE &lt;= 12 AND GEND_CD = 'W'
ORDER BY AGE DESC, PT_NAME</code></pre>
<h3 id="level-1-조건에-맞는-도서-리스트-출력하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/144853">[Level 1] 조건에 맞는 도서 리스트 출력하기</a></h3>
<pre><code class="language-sql">SELECT BOOK_ID, DATE_FORMAT(PUBLISHED_DATE, '%Y-%m-%d') AS PUBLISHED_DATE
FROM BOOK
WHERE PUBLISHED_DATE LIKE '2021%' AND CATEGORY = '인문'
ORDER BY PUBLISHED_DATE</code></pre>
<h3 id="level-1-조건에-부합하는-중고거래-댓글-조회하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/164673">[Level 1] 조건에 부합하는 중고거래 댓글 조회하기</a></h3>
<pre><code class="language-sql">SELECT B.TITLE, B.BOARD_ID, R.REPLY_ID, R.WRITER_ID, R.CONTENTS, DATE_FORMAT(R.CREATED_DATE, '%Y-%m-%d') AS CREATED_DATE
FROM USED_GOODS_BOARD AS B
JOIN USED_GOODS_REPLY AS R
ON B.BOARD_ID = R.BOARD_ID
WHERE B.CREATED_DATE LIKE '2022-10%'
ORDER BY R.CREATED_DATE, B.TITLE</code></pre>
<h3 id="level-1-모든-레코드-조회하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59034">[Level 1] 모든 레코드 조회하기</a></h3>
<pre><code class="language-sql">SELECT *
FROM ANIMAL_INS
ORDER BY ANIMAL_ID</code></pre>
<h3 id="level-1-역순-정렬하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59035">[Level 1] 역순 정렬하기</a></h3>
<pre><code class="language-sql">SELECT NAME, DATETIME
FROM ANIMAL_INS
ORDER BY ANIMAL_ID DESC</code></pre>
<h3 id="level-1-아픈-동물-찾기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59036">[Level 1] 아픈 동물 찾기</a></h3>
<pre><code class="language-sql">SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE INTAKE_CONDITION = 'Sick'
ORDER BY ANIMAL_ID</code></pre>
<h3 id="level-1-어린-동물-찾기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59037">[Level 1] 어린 동물 찾기</a></h3>
<pre><code class="language-sql">SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE INTAKE_CONDITION != 'Aged'
ORDER BY ANIMAL_ID</code></pre>
<h3 id="level-1-동물의-아이디와-이름"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59403">[Level 1] 동물의 아이디와 이름</a></h3>
<pre><code class="language-sql">SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
ORDER BY ANIMAL_ID</code></pre>
<h3 id="level-1-여러-기준으로-정렬하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59404">[Level 1] 여러 기준으로 정렬하기</a></h3>
<pre><code class="language-sql">SELECT ANIMAL_ID, NAME, DATETIME
FROM ANIMAL_INS
ORDER BY NAME, DATETIME DESC</code></pre>
<h3 id="level-1-상위-n개-레코드"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59405">[Level 1] 상위 n개 레코드</a></h3>
<pre><code class="language-sql">SELECT NAME
FROM ANIMAL_INS
ORDER BY DATETIME
LIMIT 1</code></pre>
<h3 id="level-1-조건에-맞는-회원수-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/131535">[Level 1] 조건에 맞는 회원수 구하기</a></h3>
<pre><code class="language-sql">SELECT COUNT(USER_ID) AS USERS
FROM USER_INFO
WHERE JOINED LIKE '2021%' AND AGE BETWEEN 20 AND 29</code></pre>
<h3 id="level-1-python-개발자-찾기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/276013">[Level 1] Python 개발자 찾기</a></h3>
<pre><code class="language-sql">SELECT ID, EMAIL, FIRST_NAME, LAST_NAME
FROM DEVELOPER_INFOS
WHERE SKILL_1 LIKE 'Python%' OR SKILL_2 LIKE 'Python%' OR SKILL_3 LIKE 'Python%'
ORDER BY ID</code></pre>
<h3 id="level-1-잔챙이-잡은-수-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/293258">[Level 1] 잔챙이 잡은 수 구하기</a></h3>
<pre><code class="language-sql">SELECT COUNT(ID) AS FISH_COUNT
FROM FISH_INFO
WHERE LENGTH IS NULL</code></pre>
<h3 id="level-1-가장-큰-물고기-10마리-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/298517">[Level 1] 가장 큰 물고기 10마리 구하기</a></h3>
<pre><code class="language-sql">SELECT ID, LENGTH
FROM FISH_INFO
ORDER BY LENGTH DESC, ID
LIMIT 10</code></pre>
<h3 id="level-1-특정-형질을-가지는-대장균-찾기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/301646">[Level 1] 특정 형질을 가지는 대장균 찾기</a></h3>
<pre><code class="language-sql">SELECT COUNT(ID) AS COUNT
FROM ECOLI_DATA
WHERE
    SUBSTRING(LPAD(RIGHT(CONV(GENOTYPE, 10, 2), 3), 3, '0'), 2, 1) = '0'
    AND
    (
        SUBSTRING(LPAD(RIGHT(CONV(GENOTYPE, 10, 2), 3), 3, '0'), 1, 1) = '1'
        OR
        SUBSTRING(LPAD(RIGHT(CONV(GENOTYPE, 10, 2), 3), 3, '0'), 3, 1) = '1'
    )</code></pre>