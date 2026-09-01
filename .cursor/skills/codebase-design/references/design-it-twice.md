# Design It Twice

사용자가 고른 deepening 후보의 **다른 interface**를 보고 싶을 때. Ousterhout 「Design It Twice」: 첫 안이 최선이 아닌 경우가 많아요.

어휘는 [SKILL.md](../SKILL.md). 의존 분류는 [deepening.md](deepening.md).

이 절차는 **코드 수정 없음.** `profile: game`이면 Design 단계(Architecture · Plan)에 해당해요.

## 절차

### 1. 문제 공간을 사용자에게

서브에이전트보다 먼저, 후보에 대해 짧게:

- 새 interface가 지켜야 하는 제약
- 의존과 분류 ([deepening.md](deepening.md))
- 제약을 구체화하는 **스케치** — 제안이 아니라 제약의 예시

사용자에게 보여 준 뒤 바로 2단계로 가요. 사용자가 읽는 동안 서브에이전트가 돌아가요.

### 2. 병렬 서브에이전트

Cursor **Task** `generalPurpose`를 **3개 이상** 동시에. 각자 **전혀 다른** interface.

공통 브리프: 파일 경로, 결합, deepening 분류, 시임 뒤에 둘 것. [SKILL.md](../SKILL.md) 어휘 + 프로젝트 도메인 이름(`Architecture_*` / `AGENTS.md` / README). `CONTEXT.md`를 만들지 않아요.

제약만 다르게:

- Agent 1: interface 최소화. 진입점 1–3개. 진입점당 leverage 최대
- Agent 2: 유연성. 여러 사용·확장
- Agent 3: 가장 흔한 호출자. 기본 경로를 사소하게
- Agent 4 (해당할 때만): 시임 너머 의존에 포트·어댑터 (분류 3–4, 어댑터 둘일 때)

각 출력:

1. Interface (타입, 메서드, 인자, 불변조건, 순서, 실패 모드)
2. 호출 예
3. 시임 뒤에 숨기는 구현
4. 의존 전략과 adapter ([deepening.md](deepening.md))
5. 트레이드오프: leverage가 큰 곳, 얇은 곳

### 3. 제시하고 비교

안을 하나씩 보여 준 뒤 산문으로 비교해요. **depth**(interface leverage), **locality**(변경이 모이는 곳), **seam 위치**(Architecture Boundaries)로 대비.

비교 후 **한 안을 추천**해요. 다른 안의 조각이 맞으면 하이브리드를 제안하되, 메뉴만 나열하지 않아요.

도메인 이름은 기존 Architecture / AGENTS / README에서만 가져와요. 새 용어가 필요하면 game은 Architecture 갱신을 **제안**하고, personal은 README Invariants만.
