# Contributing

여러 명이 오래 함께 쓰는 저장소입니다. 아래 흐름만 지켜주세요.

```text
Issue → Branch → 구현 / 문서 → Test → Pull Request → Review → Merge
```

## 1. Issue

모든 작업은 Issue에서 시작합니다. `chapter`, `experiment` 템플릿이 준비되어 있습니다.

- Chapter를 시작할 때: **Chapter** 템플릿 (목표, 기능/비기능 요구사항, 용량 가정, 계획한 실험)
- 가설을 검증할 때: **Experiment** 템플릿 (가설, 실험 구성, 측정 지표, 성공/실패 기준)

## 2. Branch

`<타입>/<이슈번호>-<짧은-설명>` 형태로 만듭니다.

```text
feat/1-bootstrap-spring
chapter/4-rate-limiter
experiment/4-rate-limiter-load-test
docs/4-member-notes
```

커밋 메시지에는 관련 Issue 번호를 포함합니다. 예: `feat: add token bucket limiter (#4)`

## 3. 구현 / 문서

- 설계가 정해지기 전에 코드부터 쓰지 않습니다. 요구사항 → 용량 산정 → 구조 → 트레이드오프를 먼저 정리합니다.
- 인프라/프레임워크를 새로 도입할 때는 **반드시 ADR**을 남깁니다 (`docs/architecture/adr/`).
  형식은 Context / Options / Decision / Why / Trade-offs.
- 시스템 구조가 바뀌면 `docs/architecture/current.md`와 `docs/architecture/evolution.md`를 함께 갱신합니다.
  결과만 쓰지 말고 **기존 구조로 왜 부족했는지**를 남기는 게 이 저장소의 핵심입니다.
- Chapter 문서 구조는 [docs/chapters/README.md](docs/chapters/README.md)를 따릅니다.

## 4. Test

```bash
./gradlew test
```

## 5. Pull Request

PR 템플릿의 다섯 항목을 채웁니다. "무엇을 했다"만 쓰지 않습니다.

| 항목 | 쓸 내용 |
| --- | --- |
| What | 무엇을 바꿨는지 |
| Why | 왜 이 방법인지, 어떤 요구사항/제약에서 나왔는지 |
| Learned | 이번 작업으로 새로 알게 된 것 |
| Questions & Trade-offs | 버린 대안, 아직 확신 없는 부분, 리뷰어에게 묻고 싶은 것 |
| Verification | 어떻게 확인했는지 (실행한 명령과 결과) |

본문에 `Closes #12`를 넣으면 머지될 때 Issue가 닫힙니다.
Issue가 여러 개면 `Closes #12, closes #13`처럼 키워드를 각각 붙여야 합니다.

## 6. Review

- 구현 방식보다 **설계 판단**에 대해 질문해 주세요. 이 저장소는 코드보다 판단 근거를 남기는 게 목적입니다.
- 리뷰에서 나온 중요한 논의는 PR에만 남기지 말고 해당 Chapter 문서(`defense.md` 등)로 옮깁니다.

---

## 로컬 개발 메모

### 환경 변수 (`.env`)

- `.env`는 **저장소 루트**에 두고 커밋하지 않습니다. `.env.example`을 복사해 시작하세요.
- shell 형식이 아니라 **Java properties 형식**입니다. `export` 금지, 따옴표 금지, 값에 한글 금지.
- `application.yaml`에는 `${ENV_NAME:default}` 형태로 먼저 선언하고, `.env`에는 예시 값을 추가합니다.
- ⚠️ `.env`는 `./gradlew test`에도 적용됩니다(Test task의 작업 디렉터리 = 프로젝트 루트).
  테스트 결과를 바꾸는 값은 `.env`에 두지 마세요. "로컬은 되는데 CI에서 깨지는" 원인이 됩니다.
- IntelliJ 실행 구성의 Working directory는 저장소 루트로 고정하는 게 안전합니다.

### 설정 파일

- 설정 파일은 `src/main/resources/application.yaml` **하나**만 씁니다.
  `application.properties`를 추가하면 같은 위치에서 properties가 우선하므로 조용히 덮어쓰게 됩니다.

### 문서 사이트 미리보기

```bash
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements-docs.txt
mkdocs serve
```

- 접속 주소는 <http://127.0.0.1:8000/large-scale-system-design/> 입니다
  (`site_url`의 하위 경로에 마운트되므로 루트 URL은 해당 경로로 리다이렉트됩니다).
- 배포 전 확인: `mkdocs build --strict` — CI와 동일하게 경고 하나에도 실패합니다.

### 문서를 추가할 때

- 새 페이지를 만들면 `mkdocs.yml`의 `nav`에도 추가합니다.
  반대로 **nav에 적었는데 파일이 없으면 빌드가 실패**합니다.
- 링크는 `../architecture/current.md`처럼 **상대 경로 + .md 확장자**로 씁니다.
  `/docs/...` 같은 절대 경로는 GitHub Pages 하위 경로에서 깨집니다.
- 한 디렉터리에 `index.md`와 `README.md`를 함께 두지 마세요. 충돌 경고로 빌드가 실패합니다.
- Mermaid 다이어그램은 ```` ```mermaid ```` 코드 펜스를 그대로 쓰면 됩니다.
  단, Mermaid 문법 오류는 CI가 잡지 못하므로 `mkdocs serve`로 눈으로 확인하세요.
- 책 내용을 그대로 옮겨 적지 않습니다. 우리가 이해한 것, 설계한 것, 측정한 것만 남깁니다.
