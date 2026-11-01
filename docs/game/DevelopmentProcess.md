# 개발 프로세스 (game)

game 작업에서 어떻게 진행하고, 언제 닫는지이다. 스킬이 있으면 그 체인으로 진행하고, Define·Design·착수·DoD·Build·Verify·Record·Recovery는 닫기 어휘이다. 산출물 무게는 규모에 비례한다.

Cursor: [`development-process.mdc`](../../.cursor/rules/game/development-process.mdc) · [`verification-qa-defaults.mdc`](../../.cursor/rules/game/verification-qa-defaults.mdc)  
관련: [Documentation.md](Documentation.md) · [AgentWorkflow](../common/AgentWorkflow.md)

## 진행

`.agents/skills/`가 있으면 그 스킬로 진행한다. 고를 때는 타이틀 `.agents/skills/`의 `ask-matt`를 본다. 스킬 폴더가 없으면 같은 닫기 조건을 대화로 수행한다.

| 상황 | 스킬 |
|------|------|
| 범위가 흐림 | `/grill-with-docs` |
| 여러 세션에 걸친 구현 | `/to-spec` → `/to-tickets` → 티켓마다 `/implement` |
| 한 창에서 끝나는 구현 | 그 창에서 `/implement` |
| 버그·회귀 | `/diagnosing-bugs` |
| 구현을 닫기 직전 | `/code-review` |

`/grill-with-docs`부터 `/to-tickets`까지는 한 컨텍스트에서 이어 간다. 티켓으로 나눈 뒤의 `/implement`만 티켓마다 새 컨텍스트에서 시작한다. 리팩터는 `/tdd` 루프 밖이고, `/code-review`에서 본다.

`/implement`는 `/tdd`로 합의된 seam을 한 조각씩 만들고, `/code-review`(Standards · Spec)로 닫는다. 커밋은 타이틀 `AGENTS.md`를 따른다.

`/tdd`의 red/green 실행은 사용자가 래퍼나 Test Runner로 하고 결과를 넘긴다. 에이전트는 테스트 코드를 작성하고 asmdef 컴파일만 확인한다. 실행 결과가 없어도 Build는 여기까지 닫는다. behavioral 통과는 Verify에서, 사용자가 넘긴 결과로만 판정한다.

Build 스타일(최소 diff)은 프로젝트 **`/ponytail`** 또는 AgentWorkflow §포니테일이다.

스펙·티켓은 아래 Issue tracker를 따른다. 타이틀 `AGENTS.md`가 모드를 override한다.

## 스킬 규칙 우선순위

멀티 루트(타이틀 + 이 Kit)에서 이름이 겹치면 아래 순서이다. 위가 이긴다.

1. 타이틀 `AGENTS.md` override
2. 타이틀이 명시한 오버레이 (예: `docs/plan/tickets/README.md`)
3. 타이틀 `.agents/skills/` (Matt 플로우: `/grill-with-docs` → `/to-spec` → `/to-tickets` → `/implement`)
4. 이 Kit `docs/game/` · `.cursor/rules/game/`
5. 이 Kit `docs/common/`

Matt engineering 스킬(`code-review`, `codebase-design`, `improve-codebase-architecture`)은 **Kit `.cursor/skills/`에 두지 않는다.** game Unity 각색본은 타이틀 **`.agents/skills/`** 가 정본이다. Kit Unity 전용 스킬(`unity-ecs-patterns`, `unity-build-pipeline`)만 Kit에 둔다. Kit 본문은 타이틀 repo에서 수정하지 않는다. 오버레이는 Kit 규칙을 지우는 게 아니라, Record 범위처럼 **더 구체적인 제약**을 더하는 것이다.

## Issue tracker

스펙과 구현 티켓의 정본은 이 repo의 GitHub Issues이다. `/to-spec` · `/to-tickets`의 publish는 `gh issue create`이고, `/implement`의 fetch는 `gh issue view <번호> --comments`이다. 표에 모드가 없으면 이 경로가 정본이다. 로컬 파일만 쓰려면 타이틀 `AGENTS.md` override 표의 Issue tracker 모드에 `로컬 티켓만`을 적는다.

한 세션 실험은 `.scratch/<feature-slug>/`에 둔다. 며칠 이상, 팀, 제출, Record가 필요하면 GitHub에 올린다. Architecture · 설계 정본 · ADR · `plan/Schedule.md`는 레포 문서이고, 이슈가 그 문서를 대신하지 않는다.

| 역할 | GitHub |
|------|--------|
| 스펙 | 기능당 이슈 하나. 라벨 `spec`. 본문: Problem · Stories · Out of Scope · Implementation Decisions |
| 티켓 | 이슈 하나 (합본 금지). 라벨 `ticket`. 본문 첫 줄 `Parent: #<스펙 번호>`, acceptance, 의존은 `Blocked by: #<번호>` |
| 상태 | 라벨. triage 5종과 `in-progress` ([템플릿](../../templates/docs/agents/triage-labels.md)). triage 5종의 이름만 프로젝트 말로 바꿀 수 있다 |
| 경과 | 이슈 코멘트. 날짜 · 결정 · Play · 스펙과의 차이 |

- `done`은 라벨을 붙이고 그 이슈를 닫는다. Verify를 통과하고, 구조가 바뀌었으면 Record까지 끝난 뒤이다.
- `ready-for-human` 이슈는 사람 선행만이다. 뒤 티켓의 `Blocked by`에 넣지 않는다.
- 라벨이 없으면 triage 표의 이름으로 만든다.
- `plan/Schedule.md` · `schedule/`은 macro(목표·완료 기준)이다. `/implement` 단위는 티켓 이슈이다.
- 기능 archive는 스펙 이슈를 닫는 동작이다.

뼈대: [`templates/docs/agents/issue-tracker.md`](../../templates/docs/agents/issue-tracker.md) · [`templates/docs/agents/triage-labels.md`](../../templates/docs/agents/triage-labels.md) · 타이틀 제약은 [`templates/docs/plan/tickets/README.md`](../../templates/docs/plan/tickets/README.md)

## 티켓 운영

스펙 이슈를 새로 열지, 티켓 코멘트만 쓸지, 문서를 어디까지 고칠지이다.

| 상황 | 한다 | 하지 않는다 |
|------|------|-------------|
| 계약·불변조건·입력이 바뀜 | 풀 그릴 | |
| 같은 판정, 연출만 | 짧은 그릴 또는 티켓만 | 긴 스펙을 억지로 씀 |
| 버그픽스 | 해당 티켓 이슈 코멘트 | 새 스펙 |
| 같은 What to build를 닫는 수정 | 현 티켓, 필요하면 스펙 본문 | |
| 새 유저 스토리 | 스펙 본문에 스토리 + **새 티켓 이슈** | 현 티켓 체크리스트에 몰아넣기 |
| 시행착오 | 코멘트에 날짜·결정·Play·스펙 차이 | 컴파일 일기, 완료 기준을 코드에 맞추기 |
| 다음 티켓 | 현 티켓의 behavioral 완료 기준이 닫힌 뒤 | 코드 WIP·Play 미검증으로 넘기기 |
| 하루·스프린트 끝 | 계약이 바뀐 페이지만 write-back | Architecture 일괄 재작성 |

behavioral seam(어떤 씬 Play인지)은 타이틀 `AGENTS.md`에 적는다. 새 유닛 테스트 seam은 합의 없이 열지 않는다. 계약이 바뀌면 설계 정본(GDD `locked` 또는 Technical Design)과 해당 Architecture, 필요하면 ADR을 갱신한다.

## 닫기

작은 수정은 대화 한 줄로 Define한다. Plan과 Architecture는 구조가 바뀔 때만 갱신한다. Plan 파일은 범위가 클 때만 만든다. 스펙의 Problem·Stories·In/Out이 Define이다.

| 닫힘 | 조건 |
|------|------|
| `/implement` 종료 | `/code-review`. 스킬이 없으면 변경 대조 |
| Verify | 그 작업의 Success Criteria와 「확인」. static은 리뷰. behavioral은 런타임 대조 |
| Record | 구조·계약이 바뀌면 해당 Architecture·설계 정본. 티켓 이슈가 있으면 라벨 `done` 후 닫기. 계약이 바뀐 페이지만 |
| 작업 완료 | 그 작업의 Verify. 구조가 바뀌었으면 Record까지. 티켓 이슈가 있으면 라벨 `done` 후 닫기 |

## Verify

| 유형 | 대조 |
|------|------|
| **static** | 코드·문서·asmdef 리뷰 |
| **behavioral** | Plan「확인」·런타임. 코드 리뷰만으로 pass하지 않는다 |

- Verify(대조)는 그 작업의 Success Criteria가 있으면 한다.
- Plan「확인」은 그 작업의 behavioral 완료 기준이다. 티켓에 그 기준을 적는 것은 허용한다. `Tests`·`QA`·수동 시나리오·`Test plan` 절은 사용자 요청 없이 만들지 않는다.
- 스모크·QA 러너·「테스트해 보라」제안·실행은 사용자 명시 요청 전 금지다.
- Build 중 asmdef 컴파일 등 최소 기술 확인은 한다.

## Recovery

실패하면 재시도 전에 아래 표에서 처음 해당하는 질문을 고른다.

| 질문 | 분류 | 돌아갈 곳 |
|------|------|-----------|
| 도메인·엔진 제약을 빠뜨렸는가? | 컨텍스트 | Architecture Gotchas. 규칙은 1~3줄 |
| 범위가 벗어났는가? | 방향 | `/grill-with-docs`. 스킬이 없으면 Define을 다시 고정. 필요하면 revert |
| 폴더를 어겼는가? | 구조 | Architecture·Plan을 다시 맞춘 뒤 재배치 |

별도 로그 파일은 두지 않는다. 컨텍스트·방향·구조만 Record에 한 줄 남긴다. 구현 버그는 `/diagnosing-bugs`로 고치고, 스킬이 없으면 Build에서 고친다.

Record 한 줄 형식: `Recovery: 컨텍스트 — 원인: … — 조치: …`

## 닫기 어휘

이름은 닫기 체크리스트이다. 실행은 위 진행이다.

| 어휘 | 스킬 | 닫힘 |
|------|------|------|
| Define | `/grill-with-docs`, 스펙의 Problem·Stories·Out of Scope | 사용자와 이해가 같음. 작은 수정은 대화 한 줄 |
| Design | `/to-spec`의 Implementation Decisions, Architecture | 구조 문서가 현재와 같음. 구조가 그대로면 생략 |
| 착수 | 티켓 acceptance 또는 Success Criteria, `.meta` | 티켓 이슈가 있으면 라벨 `ready-for-agent` |
| DoD | Verify. 구조·계약이 바뀌었으면 Record | 티켓 이슈가 있으면 라벨 `done` 후 닫기 |
| Build | `/implement`, `/tdd` | diff와 테스트 코드. asmdef 컴파일 확인까지. red/green은 사용자가 실행해 넘긴다 |
| Verify | `/code-review`와 그 작업의 「확인」 | Spec 축과 Success Criteria. behavioral은 사용자가 넘긴 실행 결과 |
| Record | 커밋은 타이틀 규칙. 구조·계약이 바뀌면 해당 Architecture·설계 정본·Plan | 바뀐 페이지만. 티켓 이슈는 라벨 `done` 후 닫기. archive는 스펙 이슈를 닫는 동작 |
| Recovery | `/grill-with-docs`(방향), Architecture 재배치(구조) | 컨텍스트·방향·구조만 Record 한 줄 |
