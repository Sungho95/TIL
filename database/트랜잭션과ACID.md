## 트랜잭션(Transaction)

트랜잭션이란 여러 개의 작업을 하나로 묶은 실행 유닛이다.

각 트랜잭션은 하나의 특정 작업으로 시작해서 묶여 있는 모든 작업들이 모두 완료되어야 정상적으로 종료한다.

만약, 트랜잭션에 속해있는 여러 작업 중에서 단 하나의 작업이라도 실패하면, 해당 트랜잭션에 속한 모든 작업은 실패한 것으로 판단한다.

작업이 하나라도 실패를 하게 되면 트랜잭션도 실패이고, 모든 작업이 성공적일 때만 트랜잭션이 정상적으로 실행되고 종료되는 것이다.

즉, 트랜잭션은 성공 또는 실패 두 가지 결과만 존재하며 미완료된 작업 없이 모든 작업을 성공해야 한다.

데이터베이스 트랜잭션은 ACID라는 특성을 가지고 있다.

## ACID

ACID는 데이터베이스 내에서 발생하는 하나의 트랜잭션(transaction)의 안정성을 보장하기 위해 필요한 성질이다.

**Atomicity(원자성)**

원자성은 하나의 트랜젝션 내에서 모든 연산이 성공하거나 실패하는 것을 보장하는 성질이다.

트랜잭션에 속해있는 모든 작업이 전부 성공하거나 실패해서 결과를 예측할 수 있어야 한다.

예를 들어 A 계좌에서 B 계좌로 계좌이체를 하는 트랜잭션이 있다고 가정한다면, 트랜잭션이 모두 완료 되어야만이 A와 B 계좌에서 정상적인 결과를 확인할 수 있어야 한다.

만약, A 계좌에서 이체를 하였는데, 중간에 누락이되어 실패하였다면, 해당 트랜잭션은 모두 실패되어 이체중이던 금액이 A에게 돌아와야 한다.

원자성이 보장이 안된다면 A 계좌에는 이체기록이 뜨고 금액도 차감이 되었지만, B 계좌에는 해당 기록이 안남고 결과도 반영이 안되는 등의 데이터 누락이 발생할 수 있다.

**Consistency(일관성)**

일관성은 데이터베이스의 상태가 일관되어야 한다는 성질이다. 하나의 트랜젝션 전후에 데이터베이스의 상태는 이전과 같이 유효해야 한다.

즉, 트랜잭션이 일어난 이후의 데이터베이스는 데이터베이스의 제약이나 규칙을 만족해야 한다는 뜻이다.

예를 들어, 은행의 모든 고객은 반드시 이름을 가지고 있어야 한다는 데이터베이스 제약이 있다고 가정한다면,

해당 은행에서는 이름이 없는 새로운 고객을 추가하거나, 기존 고객의 이름을 삭제하는 일이 발생해서는 안된다.

만약 이러한 상황이 발생하면 일관성을 위반하는 것이다.

데이터베이스의 유효한 상태는 서로 다를 수 있지만, 해당 상태에 대한 일관성은 변하지 않아야 한다.

**Isolation(고립성)**

고립성은 모든 트랜젝션은 다른 트랜잭션으로부터 독립적이어야 하는 성질이다.

둘 이상의 트랜젝션은 서로 어떠한 영향을 줄 수 없다.

예를 들어, A 계좌에서 B와 C로 동시에 계좌 이체를 하는 경우, 순차적으로 보내는 것과 결과가 동일해야 한다.

동시에 트랜잭션이 실행한다고 해서 B와 C에 동시에 송금하여 마이너스 통장이 발생하는 일이 없어야 한다는 것이다.

즉, 격리성을 지키는 트랜잭션은 철저히 독립적이기 때문에 다른 트랜잭션의 작업 내용을 알 수 없으며, 동시에 실행 되더라도 순차적으로 실행한 결과와 동일해야 한다.

**Durability(지속성)**

지속성은 하나의 성공된 트랜젝션에 대한 로그가 기록되고 영구적으로 남아야 하는 성질이다.

만약, 해당 트랜잭션에서 오류가 발생하더라도, 해당 기록 또한 영구적으로 남아있어야 한다.

예를 들어 은행에서 계좌에서 입출금이 발생한 이후, 해당 은행 데이터베이스에 오류가 발생하여 서버가 종료되더라도 입출금 내역은 기록으로 남아야 한다.

마찬가지로 입출금 발생하는 도중에 시스템 오류로 서버가 다운되더라도 해당 이체 내역은 실패로 돌아가고 입출금 발생 이전의 상태로 돌아가야 한다.