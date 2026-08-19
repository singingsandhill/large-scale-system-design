# 대규모 시스템 설계 기초 스터디

『가상 면접 사례로 배우는 대규모 시스템 설계 기초』를 함께 읽고,
배운 설계를 **하나의 Spring Boot 서비스**에 직접 적용해 보는 스터디 기록입니다.

Chapter마다 예제를 따로 만들지 않습니다.
초기 Spring Boot 애플리케이션 하나를 시작점으로 두고, 진행하면서 기능과 인프라를 덧붙입니다.
기술은 실제로 문제가 생겼을 때 도입하고, 그 이유를 남깁니다.

```text
Read → Design → Implement → Experiment → Defend → Document
```

## 이 사이트에서 볼 것

| 섹션 | 내용 |
| --- | --- |
| [Study](study/introduction.md) | 스터디 목적과 진행 방식, 규칙, 일정 |
| [Chapters](chapters/README.md) | Chapter별 설계 · 구현 · 실험 · 방어 기록 |
| [Architecture](architecture/current.md) | 지금 시스템이 어떤 모습인지 |
| [Evolution](architecture/evolution.md) | 시스템이 어떻게, 왜 바뀌어 왔는지 |
| [ADR](architecture/adr/README.md) | 기술 도입 결정과 그 근거 |
| [Playground](playground/README.md) | Chapter와 무관한 자유 실험 |
| [Retrospectives](retrospectives/README.md) | 회차별 회고 |

## 현재 상태

초기 Spring Boot 애플리케이션(Java 21 / Spring Boot 4.1 / H2)만 있는 상태입니다.
자세한 구조는 [Architecture](architecture/current.md)를 참고하세요.

저장소: <https://github.com/singingsandhill/large-scale-system-design>
