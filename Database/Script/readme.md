Script  

**데이터베이스**  
RDB란 무엇이고 PK, FK란 무엇인가    
데이터베이스의 기본 개념과 용어   
Join의 수행 원리를 설명해라(feat. nested join)  
파티셔닝, 샤딩, 레플리케이션이란 무엇인가  
샤딩은 무엇이고 어떤 종류가 있는지  
모듈러 샤딩 방식을 확장해야할 때 사용할 수 있는 방법에는 무엇이 있고,
어떤 Trade Off들이 있나요?  
샤딩 키 파편화 현상과 대처 방안을 알고있나?   
샤딩을 하지 말아야 할 이유는 무엇인가?  
데이터베이스 레플리케이션이 무엇이고 왜 사용하는지 아시나요?  
데이터베이스 레플리케이션의 실행 방식을 설명해주세요. (MySQL 기준)    
데이터베이스 레플리케이션시 발생하는 문제점은 무엇이 있을까요?     
레인지, 모듈러 샤딩 방식은 무엇이고 어느 장, 단점이 존재하나요?
인덱스(Index Server) 샤딩 방식에 대해서 아시나요?   
DBCP와 DBCP 튜닝(히카리풀) 커넥션 수를 측정하는법에 대해 아시는지  
Redis를 메인 DB로 사용할 수 없는 이유  
데이터베이스에서 서버 부하를 분산시키는법 클러스터링과 리플리케이션 

**정규화**  
잘못된 DB 스키마 설계가 불러오는 문제들  
Functional Dependency(함수 종속)이란    
정규화, 1NF, 2NF   
3NF, BCNF, 역정규화



**트랜잭션**  
Transcational의 ACID 속성에 대해서 아시나요?  
트랜잭션과 락의 차이, 락을 거는 이유, 락을 걸고 성능을 올리는법  
트랜잭션들이 동시에 실행될 때 isolation을 어떻게 보장하는가?  
트랜잭션들이 동시에 실행될 때 발생하는 이상 현상과 isolation의 레벨  
트랜잭션들이 동시에 실행될 때 rollback이 발생하면 어떻게 하는가?  
read lock, write rock and two-phase locking(2PL)  
2-Phase Commit이 무엇인지 아시나요?
S lock, IS lock, X lock, IX lock에 대해서 아시나요?  
Optimistic Lock에 대해서 아시나요?  
InnoDB의 Consistent Non-Locking Read 기능이 무엇인지 아시나요?  
Gap, Record, Next Key Lock에 대해서 아시나요?
분산 환경DB에서 트랜잭션 동작시 무결성 이슈가 없을까요?



**인덱스**  
index 동작 방식(B Tree 기반)  
인덱스 Scan 방식은 무엇이 있나요?  
인덱스는 크게 Hash 인덱스와 B-Tree 인덱스가 있습니다. 어떠한 차이가 있을까요?    
B-Tree 인덱스와 B+Tree 인덱스의 차이는 무엇인가요?  
클러스터 인덱스와 논클러스터 인덱스는 어떤 차이가 있나요?    
인덱스 설계시 NULL값은 고려되야 할까요? 고려해야 한다면 어떤 이유인가요?    
좋은 인덱스를 설계하기 위해 고려해야 하는 조건으로는 무엇이 있는지 아시나요?  
인덱스 적용이 어려운 요인에는 무엇이 있을까요?   
Hash index란  
Covering index란  
B tree가 인덱스 자료구조로 사용되는 이유   
NoSQL에 쓰이는 LSM 인덱스 구조에 대해 시원하게 설명해라 


**NoSQL**  
NOSQL에 대해 RDB와의 차이점?  
(RDBMS와 비교 했을 때) NoSQL가 가지는 장점은 무엇이 있을까요?  
NOSQL이 WRITE가 더 빠른 이유에 대해(데이터베이스의 DB저장 방법, LSM 트리)     
나이키, 네이버 쇼핑몰에서 Nosql인 MongoDB를 사용하는 이유  
NoSQL에서 지원하는 Transcation의 BASE에 대해서 아시나요?  
카우치베이스를 사용한 이유 몽고랑 어떤 차이가 있는지  
CAP이론에 대해 아시나요?  
Key-Value, Document, Column, Graph 저장 방식의 장단점  

https://www.notion.so/1c1c7be376d24aaf80a91a716e916026?pvs=4#dba29de5b3c64f66951c65bbdc9d1b11
