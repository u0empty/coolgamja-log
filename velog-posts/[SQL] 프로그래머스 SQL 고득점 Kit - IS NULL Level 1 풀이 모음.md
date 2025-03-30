<h3 id="level-1-경기도에-위치한-식품창고-목록-출력하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/131114">[Level 1] 경기도에 위치한 식품창고 목록 출력하기</a></h3>
<pre><code class="language-sql">SELECT WAREHOUSE_ID, WAREHOUSE_NAME, ADDRESS, COALESCE(FREEZER_YN, 'N')
FROM FOOD_WAREHOUSE
WHERE ADDRESS LIKE '경기도%'
ORDER BY WAREHOUSE_ID</code></pre>
<h3 id="level-1-이름이-없는-동물의-아이디"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59039">[Level 1] 이름이 없는 동물의 아이디</a></h3>
<pre><code class="language-sql">SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NULL</code></pre>
<h3 id="level-1-이름이-있는-동물의-아이디"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/59407">[Level 1] 이름이 있는 동물의 아이디</a></h3>
<pre><code class="language-sql">SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
ORDER BY ANIMAL_ID</code></pre>
<h3 id="level-1-나이-정보가-없는-회원-수-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/131528">[Level 1] 나이 정보가 없는 회원 수 구하기</a></h3>
<pre><code class="language-sql">SELECT COUNT(USER_ID) USERS
FROM USER_INFO
WHERE AGE IS NULL</code></pre>
<h3 id="level-1-잡은-물고기의-평균-길이-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/293259">[Level 1] 잡은 물고기의 평균 길이 구하기</a></h3>
<pre><code class="language-sql">SELECT ROUND(AVG(LENGTH), 2) AVERAGE_LENGTH
FROM (
    SELECT COALESCE(LENGTH, 10) LENGTH
    FROM FISH_INFO
) DATA</code></pre>