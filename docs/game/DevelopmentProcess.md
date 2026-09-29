# 개발 프로세스 (game)

game 작업에서 어떻게 진행하고, 언제 닫는지예요. 스킬이 있으면 그 체인으로 진행하고, Define·Design·DoD·Build·Verify·Record·Recovery는 닫기 어휘예요. 산출물 무게는 규모에 비례해요.

Cursor: [`development-process.mdc`](../../.cursor/rules/game/development-process.mdc) · [`verification-qa-defaults.mdc`](../../.cursor/rules/game/verification-qa-defaults.mdc)  
관련: [Documentation.md](Documentation.md) · [AgentWorkflow](../common/AgentWorkflow.md)

## 진행

`.agents/skills/`가 있으면 그 스킬로 진행해요. 고를 때는 타이틀 `.agents/skills/`의 `ask-matt`를 보세요. 스킬 폴더가 없으면 같은 닫기 조건을 대화로 수행해요.

| 상황 | 스킬 |
|------|------|
| 범위가 흐림 | `/grill-with-docs` |
| 여러 세션에 걸친 구현 | `/to-spec` → `/to-tickets` → 티켓마다 `/implement` |
| 한 창에서 끝나는 구현 | 그 창에서 `/implement` |
| 버그·회귀 | `/diagnosing-bugs` |
| 구현을 닫기 직전 | `/code-review` |

`/grill-with-docs`부터 `/to-tickets`까지는 한 컨텍스트에서 이어 가세요. 티켓으로 나눈 뒤의 `/implement`만 티켓마다 새 컨텍스트에서 시작하세요. 리팩터는 `/tdd` 루프 밖이고, `/code-review`에서 봐요.

`/implement`는 `/tdd`로 합의된 seam을 한 조각씩 만들고, `/code-review`(Standards · Spec)로 닫아요. 커밋은 타이틀 `AGENTS.md`를 따라요.

common **ponytail**은 Build 스타일(최소 diff)이에요.

스펙·티켓 경로와 스킬 우선순위는 아래를 따르고, 타이틀 `AGENTS.md`가 경로를 override해요.

## 스킬·규칙 우선순위

멀티 루트(타이틀 + 이 Kit)에서 이름이 겹치면 아래 순서예요. 위가 이겨요.

1. 타이틀 `AGENTS.md` override
2. 타이틀이 명시한 오버레이 (예: `docs/plan/tickets/README.md`)
3. 타이틀 `.agents/skills/` (Matt 플로우: `/grill-with-docs` → `/to-spec` → `/to-tickets` → `/implement`)
4. 이 Kit `docs/game/` · `.cursor/rules/game/`
5. 이 Kit `docs/common/`

같은 이름 스킬이 Kit와 `.agents/skills/`에 둘 다 있으면 **타이틀 `.agents/skills/`** 를 써요. Kit 본문은 타이틀 repo에서 수정하지 않아요. 오버레이는 Kit 규칙을 지우는 게 아니라, Record 범위처럼 **더 구체적인 제약**을 더하는 거예요.

## Issue tracker

GitHub Issues는 필수가 아니에요. 사용자가 명시하기 전에는 `gh issue create`로 스펙을 올리지 않아요.

| 모드 | 경로 | 적합한 때 |
|------|------|-----------|
| 임시 | `.scratch/<feature-slug>/` | 한 세션·실험 (Matt 스킬 기본) |
| 추적 | `docs/plan/tickets/<feature-slug>/` | 며칠 이상, 팀, 제출, Record가 필요할 때 |

추적 모드 레이아웃:

```text
docs/plan/tickets/<feature-slug>/
  spec.md
  issues/
    01-<slug>.md
```

- 기능당 디렉터리 하나. 티켓은 파일 하나 (합본 금지).
- 번호는 `01`부터. `Blocked by: NN`으로 의존을 적어요.
- `00`은 사람 선행만. 뒤 티켓을 막지 않아요.
- triage는 티켓 상단 `Status:` ([템플릿](../../templates/docs/agents/triage-labels.md)).
- 대화·Play 결과는 `## Comments`.
- `plan/Schedule.md` · `schedule/`은 macro(목표·완료 기준), `tickets/`는 `/implement` 단위예요.

뼈대: [`templates/docs/agents/issue-tracker.md`](../../templates/docs/agents/issue-tracker.md) · [`templates/docs/plan/tickets/README.md`](../../templates/docs/plan/tickets/README.md)

## 티켓 운영

스펙을 새로 쓸지, 티켓 Comments만 쓸지, 문서를 어디까지 고칠지예요.

| 상황 | 한다 | 하지 않는다 |
|------|------|-------------|
| 계약·불변조건·입력이 바뀜 | 풀 그릴 | |
| 같은 판정, 연출만 | 짧은 그릴 또는 티켓만 | 긴 스펙을 억지로 씀 |
| 버그픽스 | 해당 티켓 `## Comments` | 새 스펙 |
| 같은 What to build를 닫는 수정 | 현 티켓, 필요하면 스펙 | |
| 새 유저 스토리 | 스펙에 스토리 + **새 티켓** | 현 티켓 체크리스트에 몰아넣기 |
| 시행착오 | Comments에 날짜·결정·Play·스펙 차이 | 컴파일 일기, 완료 기준을 코드에 맞추기 |
| 다음 티켓 | 현 티켓의 behavioral 완료 기준이 닫힌 뒤 | 코드 WIP·Play 미검증으로 넘기기 |
| 하루·스프린트 끝 | 계약이 바뀐 페이지만 write-back | Architecture 일괄 재작성 |

behavioral seam(어떤 씬 Play인지)은 타이틀 `AGENTS.md`에 적어요. 새 유닛 테스트 seam은 합의 없이 열지 않아요. 계약이 바뀌면 설계 정본(GDD `locked` 또는 Technical Design)과 해당 Architecture, 필요하면 ADR을 갱신해요.

## 닫기

작은 수정은 대화 한 줄로 Define해요. Plan과 Architecture는 구조가 바뀔 때만 갱신해요. Plan 파일은 범위가 클 때만 만들어요. 스펙의 Problem·Stories·In/Out이 Define이에요.

| 닫힘 | 조건 |
|------|------|
| `/implement` 종료 | `/code-review`. 스킬이 없으면 변경 대조 |
| Verify | 그 작업의 Success Criteria와 「확인」. static은 리뷰. behavioral은 런타임 대조 |
| Record | 구조·계약이 바뀌면 해당 Architecture·설계 정본. Plan·티켓이 있으면 상태. 계약이 바뀐 페이지만 |
| 작업 완료 | 그 작업의 Verify. 구조가 바뀌었으면 Record까지 |

## Verify

| 유형 | 대조 |
|------|------|
| **static** | 코드·문서·asmdef 리뷰 |
| **behavioral** | Plan「확인」·런타임. 코드 리뷰만으로 pass하지 않아요 |

- Verify(대조)는 그 작업의 Success Criteria가 있으면 해요.
- 스모크·QA 러너·「테스트해보세요」제안·실행은 사용자 명시 요청 전 금지예요.
- Build 중 asmdef 컴파일 등 최소 기술 확인은 해요.

## Recovery

실패하면 재시도 전에 아래 표에서 처음 해당하는 질문을 고르세요.

| 질문 | 분류 | 돌아갈 곳 |
|------|------|-----------|
| 도메인·엔진 제약을 빠뜨렸나요? | 컨텍스트 | Architecture Gotchas. 규칙은 1~3줄 |
| 범위가 벗어났나요? | 방향 | `/grill-with-docs`. 스킬이 없으면 Define을 다시 고정. 필요하면 revert |
| 폴더를 어겼나요? | 구조 | Architecture·Plan을 다시 맞춘 뒤 재배치 |

별도 로그 파일은 두지 않아요. 컨텍스트·방향·구조만 Record에 한 줄 남겨요. 구현 버그는 `/diagnosing-bugs`로 고치고, 스킬이 없으면 Build에서 고쳐요.

Record 한 줄 형식: `Recovery: 컨텍스트 — 원인: … — 조치: …`

## 닫기 어휘

이름은 닫기 체크리스트예요. 실행은 위 진행이에요.

| 어휘 | 스킬 | 닫힘 |
|------|------|------|
| Define | `/grill-with-docs`, 스펙의 Problem·Stories·Out of Scope | 사용자와 이해가 같음. 작은 수정은 대화 한 줄 |
| Design | `/to-spec`의 Implementation Decisions, Architecture | 구조 문서가 현재와 같음. 구조가 그대로면 생략 |
| DoD | 티켓 acceptance 또는 Success Criteria, `.meta` | 티켓이 있으면 `Status: ready-for-agent` |
| Build | `/implement`, `/tdd` | diff와 seam 테스트 |
| Verify | `/code-review`와 그 작업의 「확인」 | Spec 축과 Success Criteria |
| Record | 커밋은 타이틀 규칙. 구조·계약이 바뀌면 해당 Architecture·설계 정본·Plan | 바뀐 페이지만. archive 또는 Completed |
| Recovery | `/grill-with-docs`(방향), Architecture 재배치(구조) | 컨텍스트·방향·구조만 Record 한 줄 |
