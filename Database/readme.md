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
