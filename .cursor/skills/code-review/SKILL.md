---
name: code-review
description: >-
  고정점(커밋·브랜치·태그·merge-base)부터 HEAD까지의 diff를 Standards(킷·프로젝트
  코딩 규약)와 Spec(Define/Plan/Architecture/README) 두 축으로 병렬 리뷰.
  브랜치·PR·WIP 리뷰, "since X 리뷰", game Verify static 요청 시 사용.
---

# Code Review

`HEAD`와 사용자가 준 고정점 사이 diff를 **두 축**으로 봐요. 축은 서로 컨텍스트를 섞지 않아요.

- **Standards:** 킷·프로젝트에 적힌 코딩 규약을 따르는가
- **Spec:** 이번 변경이 요청·Plan·Architecture·README가 시킨 것인가

작은 버그픽스·최소 diff를 이 스킬 이유로 리팩터하지 않아요. 포니테일이 이깁니다.

## 사용할 때

- 사용자가 브랜치·PR·WIP·「since X」리뷰를 요청할 때
- `profile: game` Verify의 **static** Success Criteria를 닫을 때

## 사용하지 않을 때

- 구현 중인 패치에 리뷰를 끼워 넣을 때
- behavioral SC를 리뷰로 pass할 때 — [DevelopmentProcess](../../../docs/game/DevelopmentProcess.md)가 이깁니다
- 아키텍처 전수 스캔 — [`improve-codebase-architecture`](../improve-codebase-architecture/SKILL.md)
- DOTS 시스템 패턴 자체 — [`unity-ecs-patterns`](../unity-ecs-patterns/SKILL.md)

## 의도를 섞지 않아요

다음을 **한 요청에** 넣으면 이 스킬을 바로 돌리지 않아요. 작업 전에 어떤 의도인지 확인해요.

- 변경분 리뷰 (Standards / Spec) → 이 스킬
- 지금 구조 설명 (as-is, 리팩터 없음) → Architecture / AGENTS / README. 전용 스킬 없음
- 리팩터 제안 (deepening 후보) → [`improve-codebase-architecture`](../improve-codebase-architecture/SKILL.md)

세 가지를 한 번에 처리하는 것은 **권장하지 않아요.** 저장소 전수·구조 맵·리팩터 제안이 같이 있으면 고정점 diff 리뷰를 시작하지 않아요. 사용자가 하나를 고를 때까지 대기해요.

```text
한 요청에 리뷰 / 구조 설명 / 리팩터 제안이 같이 있어요.
세 가지를 한 번에 하지 않는 것이 킷 권장이에요. 이번엔 어느 쪽인가요?

1. 고정점부터 diff 리뷰 (code-review)
2. 지금 구조만 설명 (리팩터 없음)
3. 아키텍처 후보만 (improve-codebase-architecture)
```

## 프로젝트 override (먼저 확인)

`AGENTS.md`와 이번 diff가 건드린 `Architecture_*` **Invariants**가 킷 기본보다 이깁니다. 문서가 허용하는 패턴은 smell로 올리지 않아요.

## 절차

### 1. 고정점

사용자가 준 ref(커밋 SHA, 브랜치, 태그, `main`, `HEAD~5` 등). 없으면 물어봐요.

확인:

- `git rev-parse <fixed-point>` 가 성공
- `git diff <fixed-point>...HEAD` (three-dot, merge-base 기준) 가 비어 있지 않음
- `git log <fixed-point>..HEAD --oneline`

잘못된 ref·빈 diff는 여기서 종료해요. 서브에이전트 안에 넣지 않아요.

### 2. Spec 출처

이 순서에서 **첫 유효한 것**:

1. 사용자가 준 경로
2. 커밋 메시지의 이슈 번호 (`#123`, `Closes #45` 등) — `gh`가 되면 본문을 가져와요. 실패해도 스킬을 중단하지 않아요. `docs/agents/issue-tracker.md`는 이 Kit에 없어요
3. `profile: game` — 브랜치·기능과 맞는 Plan, diff가 건드린 기능의 `Architecture_*`, 대화의 Define·Success Criteria
4. `profile: personal` — README Invariants, 있으면 `docs/` 한 장
5. 없음 → Spec 축을 생략하고 보고서에 `no spec available`

### 3. Standards 출처

있는 것만 읽어요.

- 킷: [`Csharp.md`](../../../docs/common/Csharp.md), 포니테일, agent-scope, naming-semantics, [`UnityBasics.md`](../../../docs/common/UnityBasics.md). 커밋 메시지 변경이면 [`CommitMessages.md`](../../../docs/common/CommitMessages.md)
- `profile: game`: Documentation, AssetsLayout, 7단계, ProjectSeparation
- `profile: personal`: DocsLite, PackageLayout
- 프로젝트: `AGENTS.md`, 이번 파일의 Architecture Invariants

그 위에 **smell 베이스라인**(아래). 두 규칙:

- **레포 문서가 이김.** 문서가 허용하면 smell을 올리지 않아요
- **전부 judgement call.** 「possible Feature Envy」처럼 라벨만. 툴이 이미 잡는 것(포맷·컴파일)은 생략

#### Smell 베이스라인

각 항목: *무엇인가* → *고치는 방향*. diff ハンク에 맞춰요.

- **Mysterious Name:** 이름만 봐선 역할이 안 보임 → 이름을 고치거나, 정직한 이름이 없으면 설계가 흐림
- **Duplicated Code:** 같은 논리 모양이 여러 ハンク·파일에 있음 → 공통 모양을 한곳으로
- **Feature Envy:** 자기 데이터보다 남의 데이터를 더 만짐 → 데이터가 있는 쪽으로 옮김
- **Data Clumps:** 같은 필드·인자 묶음이 계속 같이 다님 → 한 타입으로
- **Primitive Obsession:** 도메인 개념을 원시 타입·문자열로만 표현 → 작은 타입
- **Repeated Switches:** 같은 타입에 대한 `switch`/`if` 줄기가 diff 여러 곳에 반복 → 한곳 또는 다형성
- **Shotgun Surgery:** 한 논리 변경이 파일 여러 곳에 흩어짐 → 같이 바뀌는 것을 한 모듈로
- **Divergent Change:** 한 파일이 서로 다른 이유로 수정됨 → 이유별로 나눔
- **Speculative Generality:** spec에 없는 추상화·훅 → 지우고 인라인
- **Message Chains:** 호출자가 알 필요 없는 `a.b().c().d()` → 첫 객체에 한 메서드로
- **Middle Man:** 거의 위임만 하는 타입·함수 → 건너뛰고 실대상 호출
- **Refused Bequest:** 상속·구현이 상위 계약을 대부분 무시 → 상속 대신 구성

#### Unity에서 기본 억제

| Smell | 억제 |
|--------|------|
| Feature Envy | `transform` / `GetComponent` / `Rigidbody` 등 엔진 API |
| Primitive Obsession | `Vector3`, `float`, `int` 엔티티·레이어 ID, enum |
| Shotgun Surgery | `.cs` + 프리팹/SO + Architecture를 한 논리 변경으로 같이 고친 경우 (`.meta`는 에디터 영역 · 리뷰 대상 아님) |
| Repeated Switches | ECS 컴포넌트 타입 분기, `ISystem` 쿼리 분기 |
| Message Chains | Unity 계층 `transform.parent` 관례 |
| Data Clumps | 함께 다니는 position+rotation 등이 엔진 타입인 경우 |

### 4. 병렬 서브에이전트

Cursor **Task** `generalPurpose` 둘을 **동시에** 띄워요. 한쪽 결과를 다른쪽에 넣지 않아요.

**Standards** 프롬프트에 넣을 것:

- 전체 diff 명령과 커밋 목록
- 3단계에서 찾은 standards 파일 목록
- **smell 베이스라인 + Unity 억제 표 전문** (서브에이전트는 이 스킬을 안 봄)
- 지시: 파일/hunk마다 (a) 문서화된 규약 위반 — 파일+규칙 인용, (b) 베이스라인 smell — 이름과 ハンク. 문서 위반은 hard일 수 있으나 smell은 항상 judgement. 레포 문서가 베이스라인을 이김. 툴이 잡는 것은 생략. 400단어 안.

**Spec** 프롬프트에 넣을 것:

- diff 명령과 커밋 목록
- spec 경로 또는 가져온 본문
- 지시: (a) spec이 시켰는데 없거나 부분만, (b) spec에 없는 동작(범위 확장), (c) 구현한 것처럼 보이지만 틀린 것. 각 항목에 spec 문장을 인용. 400단어 안.

spec이 없으면 Spec Task를 띄우지 않아요.

### 5. 집계

`## Standards`와 `## Spec` 아래에 각 보고를 거의 그대로 둬요. **축을 합치거나 순위를 매기지 않아요.**

마지막 한 줄: 축별 건수, 각 축의 최악 1건(있으면). 축을 가로질러 승자를 고르지 않아요.

## 두 축인 이유

- 규약은 지키지만 잘못된 것을 구현 → Standards pass, Spec fail
- 요청은 다 했지만 프로젝트 관례를 깨뜨림 → Spec pass, Standards fail

한 축이 다른 축을 가리지 않게 나눠 둬요.

## 금지

- behavioral Success Criteria를 이 리뷰로 pass
- 스모크·QA·「테스트해보세요」·요청 없는 Test plan ([verification-qa-defaults](../../rules/game/verification-qa-defaults.mdc))
- 커밋·푸시
- 리뷰를 이유로 한 무관한 리팩터
- `.meta` 생성·수정·삭제

## 출처

[mattpocock/skills — code-review](https://github.com/mattpocock/skills/tree/HEAD/skills/engineering/code-review) (MIT, Copyright © 2026 Matt Pocock)에서 각색했어요. Kit는 spec/standards 출처를 Unity 프로필에 맞추고, Fowler smell에 Unity 억제를 더했어요. 고지: [`NOTICE`](../../../NOTICE).
