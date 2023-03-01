트랜잭션들이 동시에 실행될 때 발생하는 이상 현상에는 아래

- Dirty Read,
- Non-Repeatable Read,
- Phantom Read

각각의 이상 현상은 데이터의 불일치 문제를 일으킬 수 있습니다.

**Isolation**

은 데이터베이스에서 트랜잭션 간에 격리 수준을 설정하여, 다른 트랜잭션에서 변경한 데이터를 다른 트랜잭션에서 읽을 수 없도록 하는 것입니다. 

**Isolation 레벨**

은 네 가지가 있습니다. 각각의 격리 수준은 트랜잭션에서 발생할 수 있는 이상 현상을 제어하기 위해 정의됩니다.

- READ UNCOMMITTED,
- READ COMMITTED,
- REPEATABLE READ,
- SERIALIZABLE

**시나리오**

예를 들어, 은행에서 고객 정보를 관리하는 데이터베이스에서 A와 B 두 개의 트랜잭션이 동시에 실행될 때, A 트랜잭션이 계좌 잔액을 업데이트하는 도중에 B 트랜잭션이 같은 계좌 잔액을 조회하면 다음과 같은 이상 현상이 발생할 수 있습니다.

1. Dirty Read: A 트랜잭션이 롤백되면서 변경 내용이 취소되었지만, B 트랜잭션이 이를 읽어들이는 현상. 이 경우 B 트랜잭션은 잘못된 데이터를 읽게 됩니다.
2. Non-Repeatable Read: B 트랜잭션이 같은 계좌 잔액을 다시 조회할 때, 이전과 다른 값을 반환하는 현상. 이 경우 B 트랜잭션이 일관성 없는 데이터를 읽게 됩니다.
3. Phantom Read: A 트랜잭션이 계좌 잔액을 업데이트하는 도중에, B 트랜잭션이 새로운 계좌를 추가하는 등의 작업을 수행하면, 이전에 없던 데이터를 읽게 되는 현상. 이 경우 B 트랜잭션이 예상치 못한 데이터를 읽게 됩니다.

각각의 격리 수준에서는 이러한 이상 현상이 어느 정도 제어됩니다. 

**READ COMMITTED**

예를 들어, READ COMMITTED 격리 수준에서는 Dirty Read가 발생하지 않습니다. 하지만 Non-Repeatable Read와 Phantom Read는 발생할 수 있습니다. 

**REPEATABLE READ**

REPEATABLE READ 격리 수준에서는 Dirty Read와 Non-Repeatable Read가 발생하지 않습니다. 하지만 Phantom Read는 발생할 수 있습니다. 

**SERIALIZABLE** 

SERIALIZABLE 격리 수준에서는 이상 현상이 발생하지 않습니다.
