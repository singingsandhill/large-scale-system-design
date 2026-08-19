# 0001. 문서 스택으로 MkDocs Material 채택

- 상태: Accepted
- 날짜: 2026-08-19
- 관련: repository bootstrap

## Context

여러 명이 오래 함께 쓰는 스터디 저장소라 문서가 계속 쌓인다.
GitHub의 Markdown 렌더링만으로는 다음이 부족했다.

- 문서가 늘어나면 탐색이 어렵다 (사이드바 · 검색 없음)
- 설계 문서에 다이어그램이 필요한데, 이미지 파일을 따로 관리하고 싶지 않다
- 깨진 링크나 존재하지 않는 문서 참조를 아무도 발견하지 못한다
- 외부에 공유할 주소가 저장소 URL뿐이다

동시에 다음은 피하고 싶었다.

- 저장소 루트에 HTML을 직접 작성하는 방식 (원본이 Markdown이 아니게 됨)
- 문서 도구 학습 비용이 스터디 본 주제를 밀어내는 상황

## Options

1. **아무것도 하지 않는다** — GitHub Markdown 렌더링만 사용
2. **MkDocs + Material for MkDocs** → GitHub Actions로 GitHub Pages 배포
3. **Zensical** (Material 개발팀의 후속 정적 사이트 생성기)
4. Docusaurus / VitePress 등 JS 기반 도구

## Decision

**MkDocs + Material for MkDocs (`mkdocs-material~=9.7`)** 를 쓰고,
GitHub Actions에서 `mkdocs build --strict` 로 빌드해 GitHub Pages로 배포한다.

## Why

- 원본이 그대로 Markdown이라 GitHub에서도, 사이트에서도 읽힌다. 도구를 버려도 문서는 남는다.
- Mermaid 다이어그램이 추가 패키지 없이 코드 펜스로 동작한다. 설계 문서에 그림을 넣는 비용이 사실상 0이다.
- `--strict` 빌드가 깨진 링크 · 없는 앵커 · nav에만 있는 파일을 PR 단계에서 잡아 준다.
  문서가 조용히 썩는 것을 막는 장치가 필요했고, 이게 도입의 실질적인 이유다.
- 설정이 `mkdocs.yml` 한 파일이고, Java 개발자들이 Python 빌드 체인을 들여다볼 일이 거의 없다.
- **3번(Zensical)을 지금 쓰지 않은 이유**: 2026-08 기준 `0.0.56`으로 아직 1.0 이전이다.
  스터디 초기에 문서 도구 문제로 시간을 쓰고 싶지 않았다.
- **4번을 버린 이유**: Node 의존성과 설정 표면적이 이 저장소의 필요(문서 몇십 개)에 비해 과하다.

## Trade-offs

- ⚠️ **Material for MkDocs는 2026-11-05 EOL이다.** 현재 유지보수 모드이고, 그 이후로는
  중대 버그 · 보안 수정도 멈춘다. 즉 이 결정에는 유효기간이 있다.
- 재검토 트리거: **Zensical 1.0 출시** 또는 **2026-11** 중 먼저 오는 시점.
  Zensical은 같은 팀이 기존 Material 프로젝트와의 호환을 목표로 만들고 있어
  마이그레이션 비용은 크지 않을 것으로 본다. 그때 새 ADR을 쓰고 이 문서를 `Superseded`로 바꾼다.
- Python 툴체인이 저장소에 하나 늘어난다(`requirements-docs.txt`). CI에 job 하나 추가되는 비용.
- `--strict`가 켜져 있어, GitHub에서는 잘 보이는 문서가 CI에서 실패할 수 있다
  (절대 경로 링크, 없는 앵커 등). 규칙은 `CONTRIBUTING.md`에 적어 두었다.
- 문서 사이트는 `main` 브랜치 기준으로만 배포된다. 브랜치 작업 중에는 `mkdocs serve`로 확인해야 한다.
