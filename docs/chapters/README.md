# Chapters

Chapter별 설계 · 구현 · 실험 · 방어 기록입니다.
아직 진행한 Chapter가 없습니다. 첫 Chapter가 시작되면 아래 구조로 디렉터리를 만듭니다.

## 디렉터리 구조

```text
docs/chapters/<chapter>-<topic>/
├── index.md
├── design.md
├── implementation.md
├── experiment.md
├── defense.md
└── notes/
    └── <member>.md
```

예: `docs/chapters/04-rate-limiter/`

## 각 문서의 역할

| 파일 | 무엇을 쓰나 |
| --- | --- |
| `index.md` | Chapter 개요. 무슨 문제를 다루는지, 어디까지 했는지, 나머지 문서로 가는 링크 |
| `design.md` | 요구사항(기능/비기능) · 용량 산정 · 아키텍처 · 검토한 대안 · 트레이드오프 |
| `implementation.md` | 실제 Spring 구현과 설계의 연결. 설계 대비 **타협한 부분**을 반드시 남긴다 |
| `experiment.md` | 부하 · 장애 · 동시성 실험. 가설 → 실험 구성 → 측정값 → 결론 → 재현 방법 |
| `defense.md` | 발표에서 나온 질문과 답변. **답하지 못한 질문도 그대로 남긴다** |
| `notes/<member>.md` | 개인별 공부 내용. 형식 자유 |

## 작성 원칙

- **책 내용을 그대로 복제하지 않습니다.** 우리가 이해한 것, 설계한 것, 측정한 것만 남깁니다.
- `design.md`의 용량 산정은 결과 숫자만 적지 말고 **계산 과정**을 남깁니다.
- `experiment.md`는 측정값 없이는 완성되지 않습니다. 실행한 명령과 환경도 함께 적습니다.
- 새 기술을 도입했다면 [ADR](../architecture/adr/README.md)을 추가하고 여기서 링크합니다.
- 시스템 구조가 바뀌었다면 [Architecture](../architecture/current.md)와
  [Evolution](../architecture/evolution.md)도 함께 갱신합니다.

## 새 Chapter를 시작할 때

1. GitHub에서 **Chapter** 이슈 템플릿으로 이슈를 만듭니다.
2. `chapter/<이슈번호>-<주제>` 브랜치를 만듭니다.
3. `docs/chapters/<chapter>-<topic>/` 를 만들고 `index.md`, `design.md`부터 씁니다.
4. 만든 페이지를 `mkdocs.yml`의 `nav`에 추가합니다.
   (nav에 적었는데 파일이 없으면 문서 빌드가 실패합니다.)
