# 문서 정책 (game)

타이틀에서 어떤 문서를 만들고, Architecture와 Optimization을 어떻게 나눌지 정해요. Kit 글쓰기 공통 규칙은 [WritingGuide](../common/WritingGuide.md), personal의 README 최소 규칙은 [DocsLite](../personal/DocsLite.md)예요.

**왜 나누나요?** 현재 구조(Architecture)와 변경 이력·회귀(Optimization)를 한 파일에 섞으면, “지금 코드가 어떤지”와 “언제 왜 바뀌었는지”가 흐려져요. Plan archive는 스프린트 이관용이라 기능 Changelog를 대체하지 않아요.

이 문서는 **글쓰기·기능 문서 형식**의 정본이에요. 별도 프레임워크 process 문서(Assets·Namespace 등)를 쓰는 타이틀은 그쪽 문서를 **추가** 정본으로 둘 수 있어요. 형식·2분류·골격은 여기(Kit)를 우선하세요.

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
| ADR | `docs/**/adr/000N-<slug>.md` | 닫힌 결정·trade-off. 폴더는 첫 ADR 때 생성 |
| GDD | `gdd/` (prefix는 타이틀) | 이 Kit에 두지 않음 |
| Technical Design | `design/` (파일명은 타이틀) | GDD 없이 API·불변조건이 계약일 때. 예: `ClassStructure.md` |
| explorations / references | `explorations/` · `references/` | GDD와 분리 · 구현 근거 아님 |
| reports | `docs/**/reports/` | 주간 보고 등 — 필수 아님 |
| notes / interview | `docs/**/notes/` · `interview/` | **실행 정본 아님** · [WritingGuide](../common/WritingGuide.md) 톤 예외 |
| Process | 이 Kit `docs/game/` · common | Assets · Separation · 개발 프로세스 |

경로 prefix(`docs/` vs `Docs/`)와 타이틀 하위 폴더(`project/`, `<title>/` 등)는 타이틀이 정해요.

조사·결정·현재 구조를 한 파일에 섞지 않아요.

```text
조사 중              → investigations/
결정과 이유          → adr/
성능·회귀·변경 이력   → optimization/ (추적할 때만)
지금 구조·계약        → architecture/
```

ADR은 짧아도 돼요. 한 단락으로 “무엇을, 왜”만 적어도 돼요. 상세 조건(역전 비용·맥락 없이 보면 이상함·실제 trade-off)은 타이틀 `.agents/skills/`의 domain-modeling 스킬 `ADR-FORMAT`을 따르고, Kit에는 경로만 둬요. Investigation은 아직 열린 질문, ADR은 이미 닫힌 결정이에요.

## 씬·프리팹과 Editor

씬·프리팹·UI·`[SerializeField]` 배선의 정본과 Setup 스크립트 금지는 [UnityBasics](../common/UnityBasics.md)예요. game에서 Validator를 두면 **읽기만** 하고, 누락은 실패 메시지로 안내해요. 검증 메뉴·클래스 이름은 타이틀 `Architecture_*`에 적고, 이 Kit에 복사하지 않아요.

## 기능 문서 2분류

| 분류 | 담을 것 |
|------|---------|
| **Architecture** | 구조·경계·흐름·불변조건·변경 가이드 — Phase·주차 이력 **넣지 않음** |
| **Optimization** | Changelog(SSOT)·회귀·Go/No-go — 구조 전체 복사 **하지 않음** |

- 단순·안정 기능은 Architecture만 (Optimization 억지 생성 금지).
- Plan archive는 스프린트 이관용 — 기능 Changelog 대체 아님.
- 구조·계약 변경 → Architecture 갱신 + (있으면) Optimization Changelog **맨 위**.

## Architecture 작성 규약

제목은 `# Architecture: <Feature>`로 맞춰요.

**소제목**은 `## 한글 (English)` 형식이에요. Kit 영문 식별자는 괄호 안에 둬요.  
**목적 설명**은 각 `##` 골격 소제목 바로 아래에 **이탤릭 한 줄**로 적어요. `### 포함 범위`/`### 제외 범위`에는 넣지 않아요. 본문 lead·불릿과 구분하는 용도예요.

### 골격 (이 순서). 에디터 흐름과 관련 문서는 없으면 생략해요.

```markdown
# Architecture: <Feature>

## 개요 (Overview)

*이 기능이 **지금 무엇을 보장하는지** lead로 요약해요. 형제 Architecture 링크도 여기에 둬요.*

## 책임과 경계 (Responsibilities & Boundaries)

*이 문서가 **소유하는 범위**와 **다른 문서로 넘기는 것**을 구분해요.*

### 포함 범위 (In Scope)
### 제외 범위 (Out of Scope)

## 주요 타입과 관계 (Key Types & Relationships)

*타입 트리·관계·역할 표로 구조를 설명해요. API는 대표만 적고, enum 전수·코드 덤프는 넣지 않아요.*

## 흐름 (Flow)

*런타임·에디터에서 **어떤 순서로 동작하는지** 짧은 번호 단계로 적어요.*

### 런타임 흐름 (Runtime Flow)
### 에디터 흐름 (Editor Flow)

## 불변조건과 주의점 (Invariants & Gotchas)

*깨지면 버그인 계약과 자주 터지는 함정을 모아요.*

## 변경 가이드 (Change Guidelines)

*이 기능을 수정할 때 **확인할 체크리스트**와 **주요 코드 경로**를 둬요.*

## 관련 문서 (See also)

*같은 주제를 다루는 **다른 Architecture·Plan·Investigation** 링크예요.*
```

- **개요 (Overview)** — lead에 “이 기능이 지금 무엇을 보장하는가”. 형제 Architecture 링크.
- **책임과 경계 (Responsibilities & Boundaries)** — 소유 범위 / 다른 문서로 넘길 것. 클러스터면 경계 표 1개.
- **주요 타입과 관계 (Key Types & Relationships)** — 트리·관계·타입|역할 표. API는 대표만. enum 전수·코드 덤프 금지.
- **흐름 (Flow)** — 짧은 번호 단계. Editor 흐름이 없으면 `### 에디터 흐름 (Editor Flow)` 생략. 흐름이 여러 개면 `### 런타임 흐름 — <주제> (Runtime Flow)`처럼 한글 주제를 넣어요.
- **불변조건과 주의점 (Invariants & Gotchas)** — 깨면 버그인 계약 / 자주 터지는 함정.
- **변경 가이드 (Change Guidelines)** — 체크리스트 + 주요 코드 경로 표.
- **관련 문서 (See also)** — 관련 `Architecture_*.md` 등. 없으면 생략해요.

### 작성·갱신

- `Architecture_<Feature>Refactoring.md` = 진행 중 설계. **현재 동작 정본이 아니에요.**
- 구조·계약이 바뀐 섹션만 갱신해요. 네이밍만 바뀌면 미갱신.
- 불확실하면 「확인 필요」라고 적어요.
- 인접 기능 로직을 복사하지 마세요 — 제외 범위 + 관련 문서(See also).
- 본문은 **한국어**. 타입·경로·API·enum 식별자는 **영문 원문**.
- 분량 권장: 기능 문서가 한두 쪽을 크게 넘기면 분할하거나 Optimization으로 이관하세요 (가이드이지 강제 페이지 수는 아니에요).
- `last-verified` / 관련 asmdef 경로는 **선택** — 자주 어긋나는 페이지만.
- 폴더 README 목차와 파일 목록이 어긋나면 **README를 갱신**해요.

## Optimization 운영

### 기능 vs 횡단

| 구분 | 예 | 비고 |
|------|-----|------|
| 기능 | `Optimization_<Feature>.md` | Changelog·hot path·회귀 — Architecture와 1:1 필수는 아님 |
| 횡단 | `Optimization_Budgets` · `Optimization_ProfilingPlaybook` 등 | 팀 공통 예산·측정법 |

### 어디에 쓸지 (결정 트리)

```text
지금 당장 원인을 찾는 중인가?
  → investigations/Investigation_<주제>_….md

기능 구조를 바꾸는 다단계 작업인가?
  → architecture/Architecture_<Feature>Refactoring.md + plan/

기능 hot path·캐시·회귀·변경 이력을 장기 추적하는가?
  → optimization/Optimization_<Feature>.md (Changelog SSOT)
  → 현재 동작·계약은 architecture/Architecture_<Feature>.md

팀 횡단 예산·측정법인가?
  → optimization/ (Budgets, ProfilingPlaybook …)

캐시·hot path의 **현재 상태**만 Architecture에 반영할 때
  → Architecture 해당 절 갱신 + Optimization Changelog에 날짜 블록
```

### 권장 섹션 · 갱신

권장: Current · Hot path · Changelog(최신 위) · Decisions · 회귀 · Go/No-go · Change Guidelines.

1. **구조·계약 변경** → Architecture 갱신 + Optimization Changelog **맨 위**에 날짜 블록.
2. **성능·캐시만** → Optimization Changelog + Architecture **해당 절**만 동기화.
3. 「완료」·플랫폼 단정은 **측정·문서 상태**와 맞추세요. 기기·스테이지·proxy 제약은 타이틀 AGENTS·optimization README에 적어요.

## 설계 정본

타이틀 `AGENTS.md`에 **설계 정본 경로**를 적어요. GDD와 Technical Design 중 하나, 또는 둘 다 둘 수 있어요. 본문은 타이틀 repo에만 둬요.

| 패턴 | 경로 예 | 적합한 때 |
|------|---------|-----------|
| GDD | `gdd/` + `locked` | 기획·밸런스·스토리가 계약 |
| Technical Design | `design/ClassStructure.md` 등 | API·불변조건·클래스 구조가 계약 |

파일 이름은 타이틀이 정해요. `ClassStructure.md`는 예시예요.

- **Architecture**는 현재 구현이에요. 설계 정본 전문을 복사해 채우지 않아요.
- 외부 PDF·브리프·영상은 확인용이에요. 실행 계약은 repo 문서와 코드예요.
- 코드와 문서가 다르면 **코드가 이김**. 문서를 맞추거나, Architecture·설계 정본에 불일치를 적어요.

정본 사다리는 [WritingGuide](../common/WritingGuide.md)와 같아요. `코드 ≥ Architecture ≥ 설계 정본`.

### GDD를 쓸 때

아래는 **폴더·성숙도 태그**의 최소 공통이에요.

| 경로 | 역할 | 구현 근거? |
|------|------|------------|
| `gdd/` (또는 타이틀 override) | 확정·현재안 | **예** (`locked` / Decision) |
| `explorations/` | 가설·대안·미채택 | 아니오 |
| `references/` | 타 타이틀 조사 | 아니오 (GDD 승격 후만) |

| 태그 | 의미 |
|------|------|
| `locked` | 구현·밸런스 근거로 쓰는 확정 |
| `draft` | 가칭·후보. 약속 아님 |
| `vision` | 장기·범위 밖일 수 있음 |
| `open` | 미결 |
| `parked` | 보류·탈락 (이유 한 줄) |

구현·Play DoD·Architecture 계약의 근거는 **`locked`(또는 팀 Decision)** 만 쓰세요. Preprod→Soft Ship 일정 잠금 순서는 타이틀이 정해요.

## README 허브

- 폴더 `README.md` = 역할·목차·경계·링크·짧은 공통 규칙만. **본편 상세 금지**.
- 본편 = `Architecture_<Feature>.md`, GDD `Overview.md`, `GameName-Topic.md` 등 **문맥이 드러나는 이름**.
- **금지:** 주제만 `UI.md` / `Combat.md`. **파일이 하나뿐인 폴더**에 본편을 전부 `README.md`로 두기.
- **단일 본편 폴더:** README 없이 본편만 두고, 상위 허브는 그 파일에 **직링크**.
- **분할 폴더(본편 2+):** `README.md` = 허브만.
- Architecture **본편**에 Phase·일차·티켓 이력 표를 넣지 않아요. 진행 상태가 필요하면 `architecture/README.md` 허브의 짧은 상태표, 또는 Plan·티켓에 둬요.

### 예외

| 경로 | 이유 |
|------|------|
| repo 루트 README | 제품·클론 소개 |
| `AGENTS.md` | 에이전트 진입 |
| `notes/` · `interview/` | 학습·면접 — 실행 정본 아님 · README 허브 규칙 비적용 가능 |
| Assets 안 짧은 README | 스튜디오 Assets 규칙 |

## enum · ID

문서에 enum·상수·ID **전체 목록을 복사하지 않아요** — 코드·SO가 정본이에요.
