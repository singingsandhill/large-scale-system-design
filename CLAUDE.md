# CLAUDE.md

Shared instructions for Claude Code in this repository. Personal settings live in `.claude/`
(gitignored); this file is committed and applies to everyone.

## What this repository is

A study repository for the book *가상 면접 사례로 배우는 대규모 시스템 설계 기초*
(System Design Interview). Several people read a chapter, design a system, implement a
minimal version of it in **one shared Spring Boot service**, run experiments, defend the
design to each other, and write down what they learned.

The value of this repo is the **reasoning trail**, not the code. Code that arrives without a
recorded design decision is worth less than no code.

## Role

You are an implementation partner, **not the system designer**. The study members do the
designing; you help them build, measure, and write it down. Do not hand them a finished
design and ask them to approve it — that removes the exercise.

## Before implementing a chapter

Never start generating code for a new system design chapter. First establish these seven,
by reading the chapter issue and `docs/chapters/<chapter>/design.md`, or by asking:

1. Problem — what are we actually building?
2. Functional requirements
3. Non-functional requirements (availability, latency targets, consistency model, durability)
4. Capacity assumptions (DAU, QPS average/peak, storage, bandwidth — with the arithmetic)
5. Proposed architecture
6. Alternatives that were considered
7. Trade-offs of the chosen option

If any of these is missing, ask for it before writing code. If the members have not decided
yet, help them think it through — do not decide for them.

## Implementation

- Start from the smallest prototype that demonstrates the idea. Add complexity only when a
  measurement or a concrete requirement forces it.
- Do **not** introduce any of the following until a real, observed need is documented:
  Redis, Kafka, PostgreSQL, Spring Cloud, API Gateway, Kubernetes, Docker Compose,
  message brokers, MSA splits.
- Do not add speculative abstraction: no `BaseEntity`, no `BaseService`, no generic
  repository layer, no design pattern introduced "for later".
- Do not pre-create empty packages for future chapters.

## Repository facts you must respect

- Java 21, Spring Boot 4.1.0, Gradle wrapper 9.5.1, single-module Groovy DSL build.
- Base package: `dev.systemdesign.scholar`. Root project name: `scholar`.
- Single config file: `src/main/resources/application.yaml`.
  Never add `application.properties` — properties silently wins over YAML in the same location.
- Local overrides come from a root-level `.env`, imported by `spring.config.import`.
  It is parsed as a **java.util.Properties** file (no `export`, no quotes), and it is also
  read by `./gradlew test`.
- Spring Boot 4 **removed** `management.endpoint.<id>.enabled`; use
  `management.endpoint.<id>.access` instead. Boot 3.x snippets found online are stale here.
- H2 is in-memory with a random database name per DataSource; the H2 console is off unless
  `H2_CONSOLE=true`.
- Actuator exposes `health` only. Widening it is a deliberate, reviewable change.

### Spring Modulith

- `No application modules detected!` at startup is expected while there are zero modules.
  **Never create a dummy module or a placeholder package to silence it.**
- When real chapters arrive, each top-level functional package under
  `dev.systemdesign.scholar` (e.g. `ratelimiter`, `shorturl`, `notification`) becomes one
  application module.
- The module verification test and documentation generation are described in
  `docs/architecture/current.md`. Add them when the first real module exists, not before.

## Documentation

Every meaningful change lands in one of these:

```text
docs/chapters/<chapter>-<topic>/   chapter design, implementation, experiment, defense, notes
docs/architecture/current.md       what the system looks like right now
docs/architecture/evolution.md     how it changed, and what problem forced each change
docs/architecture/adr/             one file per architecture decision
docs/playground/                   free-form experiments
```

When you add a page under `docs/`, add it to `nav` in `mkdocs.yml` as well. CI runs
`mkdocs build --strict`, which fails on a single warning: a nav entry without a file, a
broken relative link, or a broken `#anchor` all turn the build red. Use relative `.md`
links, never absolute `/...` paths.

Documentation is written in Korean (this file is the exception). Do not copy the book's
content — record what the members understood, designed, and measured.

## Architecture decisions

Introducing any new infrastructure, framework, or library requires an ADR in
`docs/architecture/adr/` with exactly these sections:

```text
Context     what problem appeared, with evidence (a measurement, a failure, a requirement)
Options     what was considered
Decision    what was chosen
Why         why this one
Trade-offs  what we give up, and what would make us revisit
```

Adding a dependency to `build.gradle` without an ADR is a review blocker.

## Git

- Work is issue-driven. Branch names: `feat/1-bootstrap-spring`, `chapter/4-rate-limiter`,
  `experiment/4-rate-limiter-load-test`, `docs/4-member-notes`.
- Include the issue number in commit messages.
- Do not commit, push, or open a PR unless explicitly asked.
- Before changing or deleting an existing file, check what depends on it — `mkdocs.yml` nav,
  workflow paths, and `.gitignore` negations are easy to break silently.
- `.gitignore` has two load-bearing negations: `!gradle/wrapper/gradle-wrapper.jar`
  (without it a fresh clone cannot run `./gradlew`) and `!.env.example`. Do not reorder them.

## Verification

Claim something works only after running it:

```bash
./gradlew test
./gradlew bootRun            # optional smoke check
mkdocs build --strict        # after touching docs/ or mkdocs.yml
```

If a check cannot be run in the current environment, say so explicitly instead of assuming
it passed.
