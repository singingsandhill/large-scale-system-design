# Large Scale System Design

## About

『가상 면접 사례로 배우는 대규모 시스템 설계 기초』를 기반으로
대규모 시스템 설계를 공부하고, 실제 Spring Boot 서비스에 적용해 보는 스터디입니다.

Chapter별로 예제를 따로 만들지 않습니다. **하나의 서비스**를 시작점으로 두고,
Chapter를 진행하면서 기능과 인프라를 점진적으로 추가합니다.
기술은 실제 문제와 필요성이 확인됐을 때 도입하고, 그 이유를 ADR과 문서 사이트에 남깁니다.

## Principles

```text
Read → Design → Implement → Experiment → Defend → Document
```

## Tech Stack

- Java 21
- Spring Boot 4.1.0
- Gradle (wrapper 9.5.1)
- Spring Web (MVC), Validation, Actuator
- Spring Data JPA, H2 (in-memory)
- Spring Modulith
- Lombok

Redis, Kafka, PostgreSQL 등 인프라는 각 Chapter에서 **필요성이 확인되면** 추가합니다.

## Run

```bash
./gradlew test
./gradlew bootRun
```

기본 포트는 8080입니다. 로컬 설정은 저장소 루트의 `.env`로 덮어쓸 수 있습니다
(`.env.example` 참고).

## Documentation

문서 사이트: <https://singingsandhill.github.io/large-scale-system-design/>

`docs/` 아래 Markdown이 원본이고, `main` 브랜치에 머지되면 MkDocs가 빌드해 GitHub Pages로 배포합니다.

```text
docs/study/         스터디 소개 · 규칙 · 일정
docs/chapters/      Chapter별 설계 · 구현 · 실험 · 방어 기록
docs/architecture/  현재 구조, 진화 기록, ADR
docs/playground/    자유 실험
docs/retrospectives/ 회고
```

## Contributing

작업 흐름과 브랜치 · PR 규칙은 [CONTRIBUTING.md](CONTRIBUTING.md)를 참고하세요.
