# Introduction

## 목적

이 스터디의 목표는 책을 완독하는 것이 아니라,
**설계 판단을 스스로 내리고 그 근거를 설명할 수 있게 되는 것**입니다.

그래서 매 Chapter마다 다음을 남깁니다.

- 어떤 요구사항에서 출발했는지
- 어떤 대안을 검토했고 왜 그중 하나를 골랐는지
- 실제로 만들어 보니 어땠는지 (숫자로)
- 발표에서 어떤 질문에 답하지 못했는지

## 진행 방식

```text
Read        Chapter를 읽고 각자 정리한다
   ↓
Design      요구사항 · 용량 산정 · 구조 · 트레이드오프를 문서로 만든다
   ↓
Implement   실제 Spring Boot 서비스에 최소한으로 구현한다
   ↓
Experiment  가설을 세우고 측정한다 (부하 · 장애 · 동시성)
   ↓
Defend      발표하고 질문을 받는다. 답하지 못한 질문도 그대로 기록한다
   ↓
Document    결과를 문서 사이트에 남긴다
```

## 하나의 서비스로 키운다

Chapter별로 독립된 예제 프로젝트를 만들지 않습니다.
초기 애플리케이션 하나에 기능을 계속 얹으면서, 구조가 언제 한계에 부딪히는지를 직접 겪는 것이 목적입니다.

```text
Initial Spring Boot
→ Rate Limiter
→ Consistent Hashing
→ Distributed ID
→ URL Shortener
→ Notification
→ Feed
→ Chat
→ (필요해지면) Redis / Kafka / PostgreSQL
→ (필요성이 확인되면) 일부 모듈 분리 실험
```

처음부터 Redis, Kafka, MSA를 넣지 않습니다.
**"왜 지금 이게 필요한가"에 답할 수 있을 때** 도입하고, 그 답을 [ADR](../architecture/adr/README.md)에 남깁니다.

## 기록 원칙

- 책 내용을 그대로 옮겨 적지 않습니다. 우리가 이해한 것, 설계한 것, 측정한 것만 남깁니다.
- 측정하지 않은 주장은 근거로 치지 않습니다.
- 틀렸던 판단도 지우지 말고 남깁니다. 왜 틀렸는지가 다음 Chapter의 자산이 됩니다.

문서를 어디에 어떤 형식으로 쓰는지는 [Chapters](../chapters/README.md)를 참고하세요.
