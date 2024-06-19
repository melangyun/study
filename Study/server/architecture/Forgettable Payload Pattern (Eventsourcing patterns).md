> [!tip] Forgettable Payloads
 Like Crypto Shredding, the Forgettable Payloads technique relies on storing personal information in a separate database, far from the event store. **We only need to keep reference IDs to that external storage to retrieve personal information when needed.** When you receive the request to remove customers' personal information, you delete personal data from the external storage, leaving the event store untouched.

```JSON
// An example of event payload where we only store reference ID to the customers' personal details.
{
    "uuid": "f26164d0-2654-4434-9d88-56a9002e2d83",
    "event": "CustomerWasRegistered",
    "payload": {
        "customer_details_reference_uuid": "db4f7c6a-703c-4f94-8118-4610c8368e7b"
    }
}
```

- ==이벤트==에서 중요한 정보를 제거하고, 해당 정보를 별도의 (논리적; logical) 데이터 베이스에 저장한다.
- 중요한 데이터를 읽으려면 페이로드(payload) 데이터베이스를 쿼리해야 한다.
	올바른 권한 이 있는 소비자만 중요한 정보를 읽을 수 있도록 해야한다.

- 삭제 요청이 수신되면 페이로드 데이터베이스에서 페이로드를 제거하고, 이벤트 저장소의 이벤트를 그대로 유지한다.
	- 페이로드를 쿼리하는 소비자는 삭제된 페이로드에 대한 결과를 얻지 못한다.

---
[Eventsourcing Patterns: Forgettable Payloads](https://verraes.net/2019/05/eventsourcing-patterns-forgettable-payloads/)
[Challenges of Building GDPR Compliant Event-Sourced System](https://world.hey.com/otar/challenges-of-building-gdpr-compliant-event-sourced-system-0db251d4)

---
보안, 데이터 보호 및 컴플라이언스 요구사항을 충족하기 위해 설계된 데이터 저장방법.
데이터 수명을 제한하거나, 사용 후 데이터를 잊어버릴 수 있도록 설계된 메커니즘을 포함함. 이를 통해 민감한 데이터가 불필요하게 오랜 기간 저장되지 않도록 하고, 데이터 유출 시 피해를 최소한으로 할 수 있다.

