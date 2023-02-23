트랜잭션(Transaction)은 데이터베이스에서 논리적인 작업 단위를 의미합니다. 여러 개의 쿼리가 모여서 하나의 트랜잭션을 이루며, 트랜잭션 내에서 모든 쿼리가 성공적으로 실행되어야만 해당 트랜잭션을 완료할 수 있습니다. 그러나 여러 개의 트랜잭션이 동시에 실행될 때, 각각의 트랜잭션은 다른 트랜잭션에 영향을 줄 수 있습니다.

트랜잭션들이 동시에 실행될 때 isolation을 어떻게 보장하는가?

**Isolation** 의 특징을 이용한 Lock을 사용해서 해결할 수 있다.

isolation은 transaction이 진행되는 중간 상태의 데이터를 다른 transaction이 볼 수 없도록 보장하는 성질이다. 송금하는 사람의 계좌에서 돈은 빠져나갔는데 받는 사람의 계좌에 돈이 아직 들어가지 않은 DB 상황을 다른 transaction이 읽으면 안 된다.

**Lock**

Locking은 트랜잭션에서 사용하는 데이터에 대해 다른 트랜잭션이 접근하지 못하도록 데이터를 잠그는 방법입니다. 예를 들어, 한 트랜잭션이 특정 데이터를 업데이트할 때, 다른 트랜잭션이 해당 데이터를 읽거나 업데이트하지 못하도록 잠금을 걸 수 있습니다.

**시나리오**

A → B 20 BTC 이체  B도 본인 계좌에 30 BTC 입금 
동시에 일어날 수 있는 일이다.

데이터베이스에서 A와 B 두 개의 트랜잭션이 동시에 실행되는 경우, A 트랜잭션이 특정 고객의 정보를 업데이트할 때, 해당 고객 정보를 락(lock)으로 잠궈버린다.

**Dirty read ↔ Read Uncommitted**

일반적으로 사용되지 않지만 변경 내용이 commit과 rollback에 상관 없이 다른 트랙잭션에게 보여준다. 즉 어떤 작업이 처리 완료가 안되어도 다른 트랜잭션에서 볼수있게된다.

**Read Committed**

기본적으로 격리 수준(Shared Lock)을 사용한다. Commit이 완료된 데이터만 다른 트랜잭션에서 조회 가능하다. 동일 Transaction1 내에서 Select문의 결과값을 받고 작업 도중 만약 다른 Transaciton2에서 insert 또는 update를 했다고 가정 했을 때 Transaction1에서 같은 select에 다른 결과값이 보일 수 있는 문제가 있다.

**Repeatable Read**

MySql은 기본적으로 Shared Lock 사용하고 Non-repeatable read가 발생하지않는다. Undo 공간에 백업을 해두고 실제 레코드 값을 변경한다. 

**Serializable**

한 트랜잭션이 작업중이면 다른 트랜잭션 접근 불가능, 동시성이 중요한 DB에서는 거의 사용하지않는다 성능문제 떄문이다.

**ACID 원칙이 완벽하게 지켜지지 못하는 이유**

ACID 원칙을 strict 하게 지키려면 **동시성이 매우 떨어지기 때문**이다.

그렇기 때문에 DB 엔진은 ACID 원칙을 희생하여 동시성을 얻을 수 있는 방법을 제공한다. 바로 **transaction의 isolation level**이다. **Isolation 원칙을 덜 지키는 level을 사용할수록 문제가 발생할 가능성은 커지지만 동시에 더 높은 동시성을 얻을 수 있다**. ANSI/ISO SQL standard 에서 정의한 isolation level은 `READ UNCOMMITTED`, `READ COMMITTED`, `REPEATABLE READ`, `SERIALIZABLE`이다.

DB 엔진은 isolation level에 따라 서로 다른 locking 전략을 취한다. 요컨대, **isolation level이 높아질수록 더 많이, 더 빡빡하게 lock을 거는 것**이다. 따라서 각각의 isolation level을 언제 사용해야 하는지, 혹은 각 isolation level의 위험성은 무엇인지 알기 위해서는 각 isolation level 별 locking 전략을 파악해야 한다.

### **InnoDB의 Lock**

**Row-level Lock**

가장 기본적인 lock은 **테이블의 row마다 걸리는 row-level lock**이다. 여기에는 크게 shared lock과 exclusive lock의 두 종류가 있다.

**Shared lock(S lock)은 read에 대한 lock**이다. 일반적인 `SELECT` 쿼리는 lock을 사용하지 않고 DB를 읽어 들인다. 하지만 `SELECT ... FOR SHARE` 등 일부 `SELECT` 쿼리는 read 작업을 수행할 때 InnoDB가 각 row에 S lock을 건다.

**Exclusive lock(X lock)은 write에 대한 lock**이다. `SELECT ... FOR UPDATE`나 `UPDATE`, `DELETE` 등의 수정 쿼리를 날릴 때 각 row에 걸리는 lock이다.

요약하자면, **S lock을 사용하는 쿼리끼리는 같은 row에 접근 가능**
하다. 반면, **X lock이 걸린 row는 다른 어떠한 쿼리도 접근 불가능**
하다. “Shared”와 “exclusive”라는 이름의 의미와 정확히 일치한다.

**Record lock**

Record lock은 row가 아니라 **DB의 index record에 걸리는 lock**이다. 여기도 row-level lock과 마찬가지로 S lock과 X lock이 있다.

Record lock의 예시를 들어보겠다. `c1`이라는 column을 가진 테이블 `t`가 있다고 하자. 이때 한 transaction에서

라는 쿼리를 실행했다. 그러면 `t.c1`의 값이 10인 index에 X lock이 걸린다. 이때, 다른 transaction에서

라는 쿼리를 실행하려고 하면, 이 query 2는 우선 `t.c1 = 10`인 index record에 X lock을 걸려고 시도한다. 하지만 해당 index record에는 이미 transaction A가 query 1을 실행할 때 X lock을 건 상태이다. 

따라서 query 2는 transaction A가 commit 되거나 rollback 되기 전까지 `t.c1 = 10`인 row를 삭제할 수 없다. 이는 `DELETE` 뿐만 아니라 `INSERT`나 `UPDATE` 쿼리도 마찬가지이다.

모든 명령어에 대하여 트랜잭션의**롤백 명령이 적용되는 것은 아니다. DDL문(CREATE, DROP, ALTER, RENAME, TRUNCATE)**은 transaction의 rollback 대상이 아니다.
