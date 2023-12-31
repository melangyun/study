Two-Phase Commit (2PC)은 여러 데이터베이스 또는 시스템 간에 걸친 트랜잭션에 대한 원자성(모든 것 또는 아무것도 아닌 상태)을 보장하는 분산 트랜잭션 프로토콜입니다.
이는 <u>분산 시스템에서 트랜잭션을 조정하기 위해 설계</u> 되었습니다.
> NoSQL은 지원되지 않음

2PC 프로토콜은 두 단계로 구성됩니다:

1. **준비 단계 (Prepare Phase):**
    - 조정자(중앙 권한 또는 지정된 노드)는 모든 참여 노드에게 트랜잭션을 커밋할 준비가 되었는지 투표하도록 준비 메시지를 보냅니다.
    - 각 참여자는 "커밋에 동의" 또는 "준비를 중단" 중 하나로 응답합니다.
2. **커밋 단계 (Commit Phase):**
    - 모든 참여자가 준비 단계에서 커밋에 동의하면 조정자는 모든 참여자에게 커밋 메시지를 보냅니다.
    - 어떤 참여자라도 중단에 동의하거나 조정자가 일정 기간 내에 응답을 받지 못하면 조정자는 모든 참여자에게 중단 메시지를 보냅니다.

기본적으로 2PC 프로토콜은 모든 노드가 트랜잭션을 커밋하거나 아무 것도 하지 않아야 함을 보장하려고 합니다. 그러나 이 프로토콜은 블로킹 문제에 취약하며 실패 시 "블로킹 문제"라는 상황을 초래할 수 있다는 단점이 있습니다. 이러한 제한 사항으로 인해 Saga 패턴 및 기타 비동기 접근 방식과 같은 대안 분산 트랜잭션 모델을 탐구하는 연구가 이루어지고 있습니다.