---
name: improve-codebase-architecture
description: >-
  코드베이스에서 얕은 모듈을 깊게 만들 후보를 훑고, 채팅에 후보 카드로 제시한 뒤
  고른 항목만 제약부터 물어 본다. 사용자가 아키텍처 리뷰·구조 개선·deepening을
  요청했을 때만 사용.
disable-model-invocation: true
---

# Improve Codebase Architecture

구조 마찰을 찾아 **deepening 후보**를 보여 줘요. 목표는 검증하기 쉬운 시임과 에이전트가 찾기 쉬운 모듈이에요. **코드는 이 스킬에서 고치지 않아요.** Build는 사용자가 따로 요청한 뒤입니다.

어휘·원칙은 [`codebase-design`](../codebase-design/SKILL.md)을 **읽고** 그대로 써요 (module, interface, depth, seam, adapter, leverage, locality, 삭제 테스트, 어댑터 1 vs 2). Unity `Component`, Architecture **책임과 경계**, public API는 지우지 않아요.

도메인 이름은 `Architecture_*` / `AGENTS.md` / README에서. **`CONTEXT.md`를 만들지 않아요.** `docs/adr/`를 만들지 않아요.

## 사용할 때

- 사용자가 아키텍처 리뷰·구조 개선·deepening을 **명시**했을 때
- `profile: game` Design에서 경계가 커져 후보가 필요할 때 (사용자가 이 스킬을 요청)

## 사용하지 않을 때

- 핫픽스, 한 줄 버그픽스, 포니테일 최소 diff
- `profile: personal` 기본 작업 — 명시 요청 전 금지. Architecture/ADR 트리 생성 금지
- 「코드 좀 봐줘」— [`code-review`](../code-review/SKILL.md)
- 에이전트가 먼저 전 저장소를 스캔할 때 (`disable-model-invocation`)

## 의도를 섞지 않아요

다음을 **한 요청에** 넣으면 이 스킬을 바로 돌리지 않아요. 작업 전에 어떤 의도인지 확인해요.

- 변경분 리뷰 (Standards / Spec) → [`code-review`](../code-review/SKILL.md)
- 지금 구조 설명 (as-is, 리팩터 없음) → Architecture / AGENTS / README. 전용 스킬 없음
- 리팩터 제안 (deepening 후보) → 이 스킬

세 가지를 한 번에 처리하는 것은 **권장하지 않아요.** 「코드 좀 봐줘」만으로는 이 스킬이 아니에요. 리뷰·as-is 설명이 같이 있으면 스캔을 시작하지 않아요. 사용자가 하나를 고를 때까지 대기해요.

```text
한 요청에 리뷰 / 구조 설명 / 리팩터 제안이 같이 있어요.
세 가지를 한 번에 하지 않는 것이 킷 권장이에요. 이번엔 어느 쪽인가요?

1. 고정점부터 diff 리뷰 (code-review)
2. 지금 구조만 설명 (리팩터 없음)
3. 아키텍처 후보만 (improve-codebase-architecture)
```

## 절차

### 1. 탐색

**범위를 먼저.** 깊게 만드는 이득은 앞으로의 변경이므로, 최근에 바뀐 쪽에 가중치를 둬요.

- 사용자가 모듈·서브시스템·고통을 지정하면 그것만. 아래 추론은 생략
- 아니면 `git log --oneline`으로 핫스팟을 보고, 그 경로를 먼저. 흩어져 있으면 그다음 넓힘

**제외:** `ThirdParty/`, `Plugins/`, `Library/`, PackageCache, 이 워크스페이스에서 고치면 안 되는 **공유 패키지 소스** ([ProjectSeparation](../../../docs/game/ProjectSeparation.md)).

먼저 해당 영역의 `Architecture_*`, `AGENTS.md`, (personal이면) README를 읽어요.

그다음 Task (`explore` 또는 `generalPurpose`) 하나로 코드를 훑어요. 경직된 휴리스틱보다 마찰:

- 한 개념을 이해하려면 작은 모듈을 여러 번 오가야 하나
- interface가 구현만큼 복잡한 **shallow** 모듈인가
- 테스트하려고만 순수 함수를 쪼개서, 실제 버그는 호출 조합에 있나 (locality 없음)
- 시임을 넘어 새나
- 지금 interface로는 검증하기 어려운가

얕다 싶으면 **삭제 테스트:** 지우면 복잡도가 한곳에 모이나, 그냥 옮기기만 하나. 「모인다」가 신호예요.

### 2. 후보를 채팅에 제시

**기본 산출은 채팅 마크다운**이에요. temp HTML, Tailwind/Mermaid CDN, OS `open`은 하지 않아요. 사용자가 「HTML로 열어줘」라고 하면 그때만 `%TEMP%`에 정적 HTML을 쓰고 절대 경로를 알려 줘요. 저장소 안에는 쓰지 않아요.

후보마다 카드:

- **Files:** 관련 파일·모듈
- **Problem:** 한 문장. 무엇이 마찰인가
- **Solution:** 한 문장. 무엇이 바뀌는가 (아직 interface 스케치 없음)
- **Wins:** leverage · locality. 「이렇게 검증하기 쉬워진다」정도. **테스트 스위트 추가는 요청 전 금지**
- **강도:** `Strong` / `Worth exploring` / `Speculative`
- Architecture와 모순되면 카드에 표시. 마찰이 커서 Architecture 불변조건·주의점을 다시 열 때만. 문서가 금지한 이론상 리팩터를 나열하지 않아요

마지막에 **Top recommendation:** 무엇을 먼저 할지와 이유.

인터페이스는 아직 제안하지 않아요. 카드를 보여 준 뒤 물어요: 「어느 후보를 볼까요?」

### 3. 고른 뒤 — 인라인 질문

grilling / domain-modeling 스킬은 **이 Kit에 없어요.** 제약, 의존 분류([deepening.md](../codebase-design/references/deepening.md)), 깊은 모듈 모양, 시임 뒤, 남는 검증만 물어봐요.

결정이 굳으면:

| 상황 | 동작 |
|------|------|
| `profile: game`, 새 개념·경계 | 기존 `Architecture_*` 갱신을 **제안**. Design을 닫기 전 코드 수정 없음 |
| `profile: personal` | README Invariants만. Architecture/ADR 트리 금지 |
| 거절이 **구조적** 이유 | Architecture 주의점 또는 README에 한 줄 **제안**. `docs/adr/` 신설 금지. 「지금은 가치 없음」같은 일시적 이유는 기록하지 않음 |
| 다른 interface를 보고 싶다 | [design-it-twice.md](../codebase-design/references/design-it-twice.md) |

이 스킬은 **후보와 Design 대화**까지예요. 리팩터 구현은 사용자가 Build를 시킨 다음, 포니테일 최소 diff.

## 금지

- `CONTEXT.md` · `docs/adr/` 생성
- ThirdParty / 공유 패키지 소스를 후보 구현 대상으로
- 요청 없는 스모크·QA·테스트 스위트 제안
- 사용자가 고르기 전의 코드 변경
- `.meta` 생성·수정·삭제

## 출처

[mattpocock/skills — improve-codebase-architecture](https://github.com/mattpocock/skills/tree/HEAD/skills/engineering/improve-codebase-architecture) (MIT, Copyright © 2026 Matt Pocock)에서 각색했어요. Kit는 HTML 기본 산출·CONTEXT.md/ADR·grilling 의존을 빼고, 채팅 카드와 기존 Architecture/README만 써요. 고지: [`NOTICE`](../../../NOTICE).
