<h3 id="level-2-3월에-태어난-여성-회원-목록-출력하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/131120">[Level 2] 3월에 태어난 여성 회원 목록 출력하기</a></h3>
<pre><code class="language-sql">SELECT MEMBER_ID, MEMBER_NAME, GENDER, DATE_FORMAT(DATE_OF_BIRTH, '%Y-%m-%d') AS DATE_OF_BIRTH
FROM MEMBER_PROFILE
WHERE MONTH(DATE_OF_BIRTH) = 3 AND GENDER = 'W' AND TLNO IS NOT NULL
ORDER BY MEMBER_ID</code></pre>
<h3 id="level-2-재구매가-일어난-상품과-회원-리스트-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/131536">[Level 2] 재구매가 일어난 상품과 회원 리스트 구하기</a></h3>
<pre><code class="language-sql">SELECT USER_ID, PRODUCT_ID
FROM ONLINE_SALE
GROUP BY USER_ID, PRODUCT_ID
HAVING COUNT(*) &gt;= 2
ORDER BY USER_ID, PRODUCT_ID DESC</code></pre>
<h3 id="level-2-업그레이드-된-아이템-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/273711">[Level 2] 업그레이드 된 아이템 구하기</a></h3>
<pre><code class="language-sql">SELECT ITEM_ID, ITEM_NAME, RARITY
FROM ITEM_INFO
WHERE ITEM_ID IN (SELECT T.ITEM_ID
                  FROM ITEM_INFO I, ITEM_TREE T
                  WHERE I.ITEM_ID = T.PARENT_ITEM_ID AND I.RARITY = 'RARE')
ORDER BY ITEM_ID DESC</code></pre>
<h3 id="level-2-조건에-맞는-개발자-찾기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/276034">[Level 2] 조건에 맞는 개발자 찾기</a></h3>
<pre><code class="language-sql">SELECT D.ID, D.EMAIL, D.FIRST_NAME, D.LAST_NAME
FROM DEVELOPERS D
WHERE
    D.SKILL_CODE &amp; (SELECT CODE FROM SKILLCODES WHERE NAME = 'Python') &gt; 0
    OR
    D.SKILL_CODE &amp; (SELECT CODE FROM SKILLCODES WHERE NAME = 'C#') &gt; 0
ORDER BY D.ID;</code></pre>
<h3 id="level-2-특정-물고기를-잡은-총-수-구하기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/298518">[Level 2] 특정 물고기를 잡은 총 수 구하기</a></h3>
<pre><code class="language-sql">SELECT COUNT(ID) FISH_COUNT
FROM FISH_INFO
WHERE FISH_TYPE IN (SELECT FISH_TYPE FROM FISH_NAME_INFO WHERE FISH_NAME IN ('BASS', 'SNAPPER'))</code></pre>
<h3 id="level-2-부모의-형질을-모두-가지는-대장균-찾기"><a href="https://school.programmers.co.kr/learn/courses/30/lessons/301647">[Level 2] 부모의 형질을 모두 가지는 대장균 찾기</a></h3>
<pre><code class="language-sql">SELECT A.ID, A.GENOTYPE, B.GENOTYPE PARENT_GENOTYPE
FROM ECOLI_DATA A
JOIN ECOLI_DATA B
ON A.PARENT_ID = B.ID
WHERE A.GENOTYPE &amp; B.GENOTYPE = B.GENOTYPE
ORDER BY ID</code></pre>