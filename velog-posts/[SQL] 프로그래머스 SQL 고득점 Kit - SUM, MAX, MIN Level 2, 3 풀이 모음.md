<h3 id="level-2-가격이-제일-비싼-식품의-정보-출력하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/131115">[Level 2] 가격이 제일 비싼 식품의 정보 출력하기</a></h3>
<pre><code class="language-sql">SELECT PRODUCT_ID, PRODUCT_NAME, PRODUCT_CD, CATEGORY, PRICE
FROM FOOD_PRODUCT
ORDER BY PRICE DESC
LIMIT 1</code></pre>
<h3 id="level-2-최솟값-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59038">[Level 2] 최솟값 구하기</a></h3>
<pre><code class="language-sql">SELECT MIN(DATETIME)
FROM ANIMAL_INS</code></pre>
<h3 id="level-2-동물-수-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59406">[Level 2] 동물 수 구하기</a></h3>
<pre><code class="language-sql">SELECT COUNT(ANIMAL_ID)
FROM ANIMAL_INS</code></pre>
<h3 id="level-2-중복-제거하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59408">[Level 2] 중복 제거하기</a></h3>
<pre><code class="language-sql">SELECT COUNT(DISTINCT NAME)
FROM ANIMAL_INS</code></pre>
<h3 id="level-2-조건에-맞는-아이템들의-가격의-총합-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/273709">[Level 2] 조건에 맞는 아이템들의 가격의 총합 구하기</a></h3>
<pre><code class="language-sql">SELECT SUM(PRICE) TOTAL_PRICE
FROM ITEM_INFO
WHERE RARITY = 'LEGEND'</code></pre>
<h3 id="level-2-연도별-대장균-크기의-편차-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/299310">[Level 2] 연도별 대장균 크기의 편차 구하기 </a></h3>
<pre><code class="language-sql">SELECT
    YEAR(DIFFERENTIATION_DATE) YEAR,
    ((SELECT MAX(SIZE_OF_COLONY)
     FROM ECOLI_DATA
     WHERE YEAR(DIFFERENTIATION_DATE) = YEAR)
     - SIZE_OF_COLONY) YEAR_DEV,
    ID
FROM ECOLI_DATA
ORDER BY YEAR(DIFFERENTIATION_DATE), YEAR_DEV</code></pre>
<h3 id="level-3-물고기-종류-별-대어-찾기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/293261">[Level 3] 물고기 종류 별 대어 찾기</a></h3>
<pre><code class="language-sql">SELECT I.ID, N.FISH_NAME, I.LENGTH
FROM FISH_INFO I
JOIN FISH_NAME_INFO N
ON I.FISH_TYPE = N.FISH_TYPE
WHERE I.LENGTH = (SELECT MAX(LENGTH) FROM FISH_INFO WHERE FISH_TYPE = I.FISH_TYPE)
ORDER BY I.ID</code></pre>