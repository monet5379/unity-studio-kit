# 문서 정책 (game)

타이틀에서 어떤 문서를 만들고, Architecture와 Optimization을 어떻게 나눌지 정해요. Kit 글쓰기 공통 규칙은 [WritingGuide](../common/WritingGuide.md), personal의 README 최소 규칙은 [DocsLite](../personal/DocsLite.md)예요.

**왜 나누나요?** 현재 구조(Architecture)와 변경 이력·회귀(Optimization)를 한 파일에 섞으면, “지금 코드가 어떤지”와 “언제 왜 바뀌었는지”가 흐려져요. Plan archive는 스프린트 이관용이라 기능 Changelog를 대체하지 않아요.

Cursor: [`documentation.mdc`](../../.cursor/rules/game/documentation.mdc)

## 에이전트 위키 계약

타이틀 `docs/`는 **위키처럼** 쓰되, 통째로 컨텍스트에 넣지 않아요. 타이틀 지식은 **그 타이틀 repo**에만 두고, 이 Kit에 쌓지 않아요.

| | 규칙 |
|--|------|
| **읽을 때** | 기능 작업 전 해당 `Architecture_*`(+필요 시 GDD)만. 허브 README → 링크된 페이지만 |
| **쓸 때** | 구조·계약이 바뀌면 Architecture 갱신. Changelog·회귀면 Optimization |
| **쓰지 말 때** | 회의·면접 로그 통째 붙여넣기, enum/API 전체 복사, Notion/채팅 덤프 |
| **컨텍스트** | `docs/` 전체를 alwaysApply 하지 않음. 진입은 허브·`AGENTS.md` |

**불일치:** 코드와 문서가 다르면 **코드가 이김**. 문서는 맞추거나 “현재 구현은 계약을 충족하지 않음”을 Architecture에 명시해요.

Write-back(Verify/Record·Investigation 이관)은 [DevelopmentProcess](DevelopmentProcess.md) Record를 따르고, 경로·목차는 타이틀 `docs/**/README.md` · `AGENTS.md`가 정본이에요.

## 문서 종류

| 종류 | 위치 (관례) | 비고 |
|------|-------------|------|
| Architecture | `docs/**/architecture/Architecture_<Feature>.md` | 기능당 1파일 · **현재** 구조만 |
| Optimization | `docs/**/optimization/Optimization_<Feature>.md` | Changelog·회귀 — 지속 추적이 있을 때만 |
| Plan | `docs/**/plan/` | 구조 변경·큰 범위 |
| Investigation | `docs/**/investigations/` | 조사 1건 1파일 |
| GDD | 타이틀 `docs/**/design/gdd/` | 이 Kit에 두지 않음 |
| Process | 이 Kit `docs/game/` · common | Assets · Separation · 7단계 |

경로 prefix(`docs/` vs `Docs/`)는 타이틀이 정해요.

## 기능 문서 2분류

| 분류 | 담을 것 |
|------|---------|
| **Architecture** | 구조·경계·흐름·불변조건·변경 가이드 — Phase·주차 이력 **넣지 않음** |
| **Optimization** | Changelog(SSOT)·회귀·Go/No-go — 구조 전체 복사 **하지 않음** |

- 단순·안정 기능은 Architecture만 (Optimization 억지 생성 금지).
- Plan archive는 스프린트 이관용 — 기능 Changelog 대체 아님.
- 구조·계약 변경 → Architecture 갱신 + (있으면) Optimization Changelog **맨 위**.

## Architecture 작성 규약

### 필수 섹션

개요 · 책임과 경계 · 주요 타입과 관계 · 흐름 · 불변조건과 주의점 · 변경 가이드

### 품질

- 책임과 경계·흐름·불변조건·코드 경로(표기 관례는 타이틀)·변경 가이드를 빠뜨리지 않아요.
- `last-verified` / 관련 asmdef 경로는 **선택** — 자주 어긋나는 페이지만.
- 폴더 README 목차와 파일 목록이 어긋나면 **README를 갱신**해요.

## README 허브

- 폴더 `README.md` = 역할·목차·경계·링크만. **본편 상세 금지**.
- 본편 = `Architecture_<Feature>.md` 등 **문맥이 드러나는 이름**.
- 금지: 주제만 `UI.md` / `Combat.md`. 파일 1개 폴더에 본편을 README에 몰아넣기.
- 예외: repo 루트 README, `AGENTS.md`, Assets 안 20줄 README.

## enum · ID

문서에 enum·상수·ID **전체 목록을 복사하지 않아요** — 코드·SO가 정본이에요.
