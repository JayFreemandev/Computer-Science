Script
트랜잭션들이 동시에 실행될 때 isolation을 어떻게 보장하는가?  
트랜잭션들이 동시에 실행될 때 발생하는 이상 현상과 isolation의 레벨
recoverability. 트랜잭션들이 동시에 실행될 때 rollback이 발생하면 어떻게 하는가?
read lock, write rock and two-phase locking(2PL)
잘못된 DB 스키마 설계가 불러오는 문제들
Functional Dependency(함수 종속)이란
Functional Dependency를 바탕으로 DB 테이블을 설계하는 방법(정규화, 1NF, 2NF)
2NF, 3NF, BCNF, 역정규화
index 동작 방식
JOIN의 동작 방식
B tree가 인덱스 자료구조로 사용되는 이유
파티셔닝 샤딩 레플리케이션 
-> til  
질문 1. Replication에서 장애가 발생하여 primary가 죽으면 대기중인 secondary가 primary로 바뀌는건지 아니면 primary, secondary 개념은 그대로고 secondary가 primary 역할을 하게 되는건지?  
질문 2. 고가용성이라 해도 read/write가  primary에서 secondary로 옮겨갈 때 사용자의 입장에서 장애를 느끼나?  
1.
말씀하신 것처럼 secondary와 primary의 역할이 바뀌
2.
문제가 감지되면 진행되는 것이 fail over이기 때문에 일단 일부 기능은 정상적으로 동작하지 않아 일부 사용자는 장애를 느꼈을 수도 있다
하지만 fail over가 빠르게 일어나기 때문에 (제 직간접적인 경험으로는 빠르면 수초가 걸렸고 보통은 1분 이내 였습니다) 
대부분의 사용자들은 일시적으로 잠시 문제가 생겼다 정도 수준으로 인지되지 않을까 싶다

만약 백엔드 아키텍처를 견고하게 잘 설계 했다면 DB 앞 단에 캐시(cache)도 있을거고 리트라이 로직도 있을 수 있으니 
이런 것들까지 고려하면 사용자들의 일부가 잠깐동안 '동작이 이상하네' 수준으로 느낄거같다.

DBCP와 DBCP 튜닝(히카리풀)
NOSQL에 대해 RDB와의 차이점?
NOSQL이 WRITE가 더 빠른 이유에 대해(데이터베이스의 DB저장 방법, LSM 트리)
나이키, 네이버 쇼핑몰에서 Nosql인 MongoDB를 사용하는 이유
Redis를 메인 DB로 사용할 수 없는 이유
데이터베이스에서 서버 부하를 분산시키는법 클러스터링과 리플리케이션
인덱스는 크게 Hash 인덱스와 B-Tree 인덱스가 있습니다. 어떠한 차이가 있을까요?
B-Tree 인덱스와 B+-Tree 인덱스의 차이는 무엇인가요?
Transcational의 ACID 속성에 대해서 아시나요?
인덱스 Scan 방식은 무엇이 있나요?
클러스터 인덱스와 논클러스터 인덱스는 어떤 차이가 있나요?
인덱스 설계시 NULL값은 고려되야 할까요? 고려해야 한다면 어떤 이유인가요?
좋은 인덱스를 설계하기 위해 고려해야 하는 조건으로는 무엇이 있는지 아시나요?
인덱스 적용이 어려운 요인에는 무엇이 있을까요?
Nested Loop 조인은 무엇일까요?
데이터베이스 레플리케이션이 무엇이고 왜 사용하는지 아시나요?
데이터베이스 레플리케이션의 실행 방식을 설명해주세요. (MySQL 기준)
데이터베이스 레플리케이션시 발생하는 문제점은 무엇이 있을까요?
데이터베이스 샤딩은 무엇이고 어떤 종류가 있는지 아시는데로 말씀해주세요.
레인지, 모듈러 샤딩 방식은 무엇이고 어느 장, 단점이 존재하나요?
모듈러 샤딩 방식을 확장해야할 때 사용할 수 있는 방법에는 무엇이 있고, 어떤 Trade Off들이 있나요?
인덱스(Index Server) 샤딩 방식에 대해서 아시나요?
2-Phase Commit이 무엇인지 아시나요?
S lock, IS lock, X lock, IX lock에 대해서 아시나요?
Optimistic Lock에 대해서 아시나요?
InnoDB의 Consistent Non-Locking Read 기능이 무엇인지 아시나요?
Gap, Record, Next Key Lock에 대해서 아시나요?
많은 사용자들에게 News feed를 제공하는 서비스가 있고, 주간 인기 Feed를 보여주는 것과 일간 Feed를 보여주는 페이지가 있다고 가정할 많은 량의 읽기 트래픽이 존재한다면 어떻게 대처할 수 있을지 말씀해보세요. (주간 인기 Feed에 대한 대처와 일간 Feed에 대한 대처)
(RDBMS와 비교 했을 때) NoSQL가 가지는 장점은 무엇이 있을까요?
NoSQL에서 지원하는 Transcation의 BASE에 대해서 아시나요?
MongoDB의 Compound-key Index란 무엇인가요?
MongoDB의 Compound-key Index 선언 시 효율을 높이기 위해서 포함하는 필드 순서를 어떻게 정의하면 좋을까요?
Write Conflict 발생 시 MongoDB는 어떻게 이를 해결하려고 시도할까요?
readConcern Option은 어떠한 이점을 제공할까요? (read staleness)
readConcern Option의 linerizable과 majority 속성은 어떤 차이가 있나요?
writeConcern Option은 어떠한 이점을 제공할까요?
replicaset을 구성할 때 buildIndexes false로 설정하는 경우는 어떤 것을 위해서 사용하는 것인가요?
MongoDB Cluster의 구성 요소로는 무엇이 있나요?
Journaling은 무엇이고, MongoDB의 Journal은 어떠한 방식으로 구현되어 있나요?
