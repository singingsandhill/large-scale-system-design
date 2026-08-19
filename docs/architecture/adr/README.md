# Architecture Decision Records

새로운 인프라 · 프레임워크 · 라이브러리를 도입하거나, 되돌리기 어려운 구조 결정을 내릴 때
파일 하나를 남깁니다. 결정 자체보다 **그때 무엇을 알고 있었는지**를 남기는 게 목적입니다.

## 목록

| 번호 | 제목 | 상태 | 날짜 |
| --- | --- | --- | --- |
| [0001](0001-documentation-stack.md) | 문서 스택으로 MkDocs Material 채택 | Accepted | 2026-08-19 |

## 규칙

- 파일 이름: `NNNN-kebab-case-title.md` (번호는 4자리, 순차 증가)
- 상태: `Proposed` / `Accepted` / `Superseded by NNNN` / `Deprecated`
- 한 번 머지된 ADR은 **수정하지 않습니다.** 생각이 바뀌면 새 ADR을 쓰고
  이전 것의 상태를 `Superseded by NNNN`으로 바꿉니다.
- `build.gradle`에 의존성을 추가하는 PR은 ADR 없이 머지하지 않습니다.

## 템플릿

```markdown
# NNNN. <제목>

- 상태: Proposed | Accepted | Superseded by NNNN
- 날짜: YYYY-MM-DD
- 관련: #이슈번호, Chapter N

## Context

어떤 문제가 생겼는가. 가능하면 측정값이나 구체적인 실패 사례로. "좋아 보여서"는 Context가 아니다.

## Options

검토한 선택지들. 하지 않는 것(do nothing)도 하나의 선택지다.

## Decision

무엇을 선택했는가.

## Why

왜 그것인가. 다른 선택지를 왜 버렸는가.

## Trade-offs

이 선택으로 무엇을 포기했는가. 어떤 조건이 생기면 이 결정을 다시 볼 것인가.
```
