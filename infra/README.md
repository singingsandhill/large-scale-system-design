# infra

로컬 실행에 필요한 인프라 정의를 두는 자리입니다. **지금은 비어 있고, 그게 정상입니다.**

현재 시스템은 Spring Boot 애플리케이션 하나 + 인메모리 H2뿐이라
컨테이너도, 외부 의존성도 필요하지 않습니다.

## 언제 채우나

Chapter를 진행하다 실제로 필요해졌을 때만 추가합니다. 예를 들면,

- 인스턴스를 2대 이상 띄우는 실험을 하려는데 상태 공유가 필요해졌을 때 → Redis
- 비동기 처리를 실제로 확인해야 할 때 → 메시지 브로커
- H2로는 재현되지 않는 동작을 확인해야 할 때 → PostgreSQL

추가할 때는 반드시 함께 남깁니다.

1. [ADR](../docs/architecture/adr/README.md) — Context / Options / Decision / Why / Trade-offs
2. [Evolution](../docs/architecture/evolution.md) — 기존 구조로 왜 부족했는지
3. 이 디렉터리의 README — 실행 방법과 필요한 포트

"나중에 쓸 것 같아서" 미리 넣지 않습니다.
