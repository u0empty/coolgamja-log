<h2 id="aws-카테고리별-서비스">AWS 카테고리별 서비스</h2>
<ul>
<li>관계형: RDS, Amazon Aurora, Amazon Redshift</li>
<li>키-값: DynamoDB</li>
<li>문서: DocumentDB</li>
<li>인메모리: ElasticCache, MemoryDB For Redis</li>
<li>그래프: Amazon Neptune</li>
<li>타임시리즈: Timestream</li>
<li>원장(Ledger): Amazon QLDB(Quantum Ledger Database)</li>
<li>검색: Elasticsearch Service</li>
</ul>
<h2 id="1-관계형-데이터베이스">1. 관계형 데이터베이스</h2>
<p><strong>데이터의 관계에 집중한 데이터베이스</strong></p>
<ul>
<li>사전에 정의된 데이터 간 관계가 있을 때 사용</li>
<li>미리 지정된 형식과 타입의 데이터만 (스키마에)저장 가능</li>
</ul>
<p><strong>테이블 형식으로 데이터 관리</strong></p>
<ul>
<li>행과 열을 기반으로 한 여러 테이블을 통해 데이터 정의</li>
<li>고유의 키로 각 데이터를 식별</li>
</ul>
<p><strong>트랜잭션 지원</strong></p>
<ul>
<li>원하는 동작이 <code>정확히 수행 or 완전히 실패</code> 둘 중 하나로 유지</li>
<li>일부 반영 혹은 실패했지만 데이터 변경이 되는 등 애매한 상태는 없음</li>
<li>일반적인 어플리케이션, 온라인 게임 등에 사용</li>
</ul>
<h3 id="oltponline-transactional-processing">OLTP(Online Transactional Processing)</h3>
<blockquote>
<p>주로 데이터의 트랜잭션을 다루는 데이터베이스</p>
</blockquote>
<p>ex) id가 1인 사용자의 이름, 나이 조회 or 값 수정</p>
<ul>
<li>주로 관계형 데이터베이스에서 처리</li>
<li>행 단위에 관심</li>
<li>Amazon RDS</li>
</ul>
<h3 id="olaponline-analytical-processing">OLAP(Online Analytical Processing)</h3>
<blockquote>
<p>데이터를 종합적으로 보고 통계를 산출하는데 특화된 데이터베이스</p>
</blockquote>
<p>ex) 1월 한 달간 오리에서 가장 많이 팔린 붕어빵 종류 조회</p>
<ul>
<li>주로 데이터 웨어하우스에서 처리</li>
<li>열 단위에 관심</li>
<li>Amazon Redshift</li>
</ul>
<h3 id="관계형-데이터베이스-정리">관계형 데이터베이스 정리</h3>
<ul>
<li>기존 DB를 마이그레이션하는 경우: Amazon RDS(MySQL, PostreSQL, Oracle, MS SQL 등)</li>
<li>처음부터 관계형 DB를 사용하며 클라우드를 위한 설계를 반영하여 AWS스러운 DB 쓰겠다: Amazon Aurora </li>
<li>데이터 웨어하우스(OLAP): Amazon Redshift</li>
</ul>
<h2 id="2-키-값-데이터베이스">2. 키-값 데이터베이스</h2>
<p><strong>데이터를 단순히 키-값으로 정의</strong></p>
<ul>
<li>키를 고유한 식별자로 사용하는 키-값 쌍의 집합으로 데이터 저장</li>
<li>파티셔닝 가능, 다른 유형의 데이터베이스로는 안되는 범위까지 수평 확장 가능</li>
<li>키만 사용해서 쿼리 가능</li>
<li>세션 저장(유저 로그인 인증 등에 사용), 많은 양의 데이터(장바구니 등)를 관리할 때</li>
</ul>
<h3 id="dynamodb">DynamoDB</h3>
<ul>
<li>NoSQL방식으로 미리 지정된 형식이 필요없어 데이터 형식이 자유로움</li>
<li>파티션키, 정렬키, 기타 속성명 존재</li>
<li>기본값(NULL 등) 없이 빈 값도 가능</li>
</ul>
<h2 id="3-문서-데이터베이스">3. 문서 데이터베이스</h2>
<ul>
<li>데이터를 JSON 등의 문서로 데이터를 저장 및 쿼리</li>
<li>각 어플리케이션에서 사용하는 모델 형식을 그대로 사용 가능 ex) JS의 JSON 등</li>
<li>Next된 구조로 문서 저장 가능</li>
<li>비디오나 블로그 등의 컨텐츠 관리, 제품 카탈로그 저장 등</li>
<li>Amazon DocumentDB(MongoDB 호환)</li>
</ul>
<h2 id="4-그래프-데이터베이스">4. 그래프 데이터베이스</h2>
<p><strong>데이터보다 데이터 간 관계가 더 중심인 데이터베이스</strong></p>
<ul>
<li>각 데이터 주체 간 관계와 연결을 분석하는 데 최적화되어 있다.</li>
<li>SNS, 이상 탐지, 추천 엔진 등에 사용</li>
</ul>
<h2 id="5-인-메모리-데이터베이스">5. 인-메모리 데이터베이스</h2>
<p><strong>메모리를 사용한 데이터베이스</strong></p>
<ul>
<li>SSD나 하드디스크가 아닌 메모리에 저장하므로 읽기/쓰기가 매우 빠름</li>
<li>SSD나 하드디스크에 비해서는 내구성이 떨어짐</li>
<li>실시간 경매, 게임 랭킹 보드, 캐싱(자주 요청되는 메인 DB의 쿼리를 임시로 저장했다가 빠르게 제공) 등에 사용</li>
<li>Amazon MemoryDB: 내구성까지 확보한 인-메모리 데이터베이스 서비스</li>
</ul>
<h3 id="amazon-memorydb-vs-elasticache">Amazon MemoryDB vs ElastiCache</h3>
<ul>
<li><p>ElastiCache</p>
<ul>
<li>메인DB의 워크로드를 분산하고 캐싱 기능으로 활용</li>
<li>쿼리 캐싱, 세션 저장, 임시 데이터 저장 등에 사용</li>
</ul>
</li>
<li><p>Amazon MemoryDB</p>
<ul>
<li>메모리DB로 메인DB 자체로 사용을 상정</li>
<li>타임시리즈 DB, IoT 기기의 메인DB 등으로 사용</li>
</ul>
</li>
</ul>
<h2 id="6-검색-데이터베이스">6. 검색 데이터베이스</h2>
<p><strong>데이터 검색에 특화된 데이터베이스</strong></p>
<ul>
<li>인덱싱과 카테고리 기능에 특화</li>
<li>목표: 원하는 데이터를 빠르게 찾는 것</li>
<li>저장을 위한 데이터베이스 외의 특별한 목적으로 사용됨</li>
<li>로그 검색, 유저 정보 검색 등 컨텐츠 검색이나 로그 분석 등에 사용</li>
<li>Amazon Elasticsearch Service</li>
</ul>
<h2 id="7-원장ledger-데이터베이스">7. 원장(Ledger) 데이터베이스</h2>
<p><strong>데이터의 신뢰성 및 투명성이 중요한 데이터베이스</strong></p>
<ul>
<li>장부</li>
<li>중심 기능: 데이터의 정확한 변경 내역 및 무결성 확보</li>
<li>블록체인 네트워크 및 암호화로 무결성 확보</li>
<li>금융 거래 기록 등에 사용</li>
</ul>
<h2 id="8-타임시리즈-데이터베이스">8. 타임시리즈 데이터베이스</h2>
<p><strong>많은 이벤트를 시간단위로 저장하기 위한 데이터베이스</strong></p>
<ul>
<li>수만~수십만건의 이벤트 데이터를 시간에 따라 정렬하고 특정 시점의 이벤트를 쿼리</li>
<li>많은 IO 발생</li>
<li>IoT 기기의 이벤트 관리, 분석 어플리케이션에 사용</li>
</ul>
<p><br />뭐가 증말 많네..</p>
<hr />
<h2 id="reference">Reference</h2>
<ul>
<li><a href="https://youtu.be/mRBpWLssAZQ?si=nEAY4ShfYXgrj7Ua">AWS 카테고리별 데이터베이스 정리</a></li>
</ul>