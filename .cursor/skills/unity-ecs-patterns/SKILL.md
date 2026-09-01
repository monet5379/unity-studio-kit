---
name: unity-ecs-patterns
description: >-
  Unity DOTS(Entities, Jobs, Burst) 생산 패턴 — ISystem, ECB, query, Aspect,
  baking, Native collection. data-oriented 시스템, CPU bound 시뮬, 대량 entity,
  OOP→ECS 전환, ISystem/ECB/Baker/IJobEntity 작업 시 사용.
---

# Unity ECS Patterns

Unity DOTS(Data-Oriented Technology Stack) — Entity Component System, Job System, Burst Compiler 생산 패턴이에요.

## 사용할 때

- 고성능 Unity 게임·시뮬레이션을 만들 때
- 수천 개 entity를 효율적으로 다룰 때
- data-oriented 게임 시스템을 구현할 때
- CPU bound 로직을 최적화할 때
- OOP 코드를 ECS로 옮길 때
- Jobs·Burst로 병렬화할 때
- DOTS, Entities, ISystem, ECB, Baker, IJobEntity를 언급할 때

## 사용하지 않을 때

- MonoBehaviour만 쓰는 UI·씬 흐름·비시뮬 코드
- ECS 성능·아키텍처와 무관한 작업

## 프로젝트 override (먼저 확인)

워크스페이스에 **Architecture_*** 문서나 `AGENTS.md` ECS override가 있으면:

- hybrid 경계, system group, subscene, Entities package pin은 **프로젝트 Architecture가 이깁니다**
- 이 skill은 **범용 DOTS 패턴**만 제공해요. 샘플 타입명(`EnemyTag`, `GameConfig` 등)을 도메인 문서 없이 그대로 복사하지 마세요

## 핵심 개념

### ECS vs OOP

| 항목 | 기존 OOP | ECS/DOTS |
| ---- | -------- | -------- |
| 데이터 배치 | 객체 지향 | data-oriented |
| 메모리 | 분산 | 연속(contiguous) |
| 처리 | 객체마다 | 배치(batch) |
| 확장 | 수가 늘면 불리 | entity 수에 거의 선형 |
| 적합 | 복잡한 단일 행위 | 대량 시뮬레이션 |

### DOTS 용어

```text
Entity: 가벼운 ID (데이터 없음)
Component: 순수 데이터 (행위 없음)
System: component를 처리하는 로직
World: entity를 담는 컨테이너
Archetype: component 조합의 유일한 형태
Chunk: 같은 archetype entity의 메모리 블록
```

## 모범 사례

### Do

- **SystemBase보다 ISystem** — 성능·Burst 친화
- **hot path는 BurstCompile** — 체감 속도 차이 큼
- **structural change는 ECB로 묶기** — sync point 최소화
- **Profiler로 프로파일** — 병목부터 확인
- **Aspect로 component 묶기** — query·접근 정리
- **Persistent Native collection은 Dispose** — system/world 종료 시

### Don't

- **Burst 경로에 managed 타입** 금지
- **job/foreach 안에서 structural change** 금지 → ECB
- **과도한 설계** 금지 — 먼저 단순하게
- **chunk utilization 무시** 금지 — 비슷한 entity끼리 묶기
- **Native dispose 누락** 금지 — 누수 남

## 상세 패턴

Pattern 1(component) ~ Pattern 8(Native collection)과 performance tips:

→ [references/details.md](references/details.md)

ECS 코드를 구현·리뷰할 때 위 파일을 읽어요. 이 파일만으로는 코드 생성에 부족합니다.

## 검증

ECS 변경 후:

- 관련 asmdef 컴파일 (Entities, Burst, Mathematics, Transforms 등)
- hot loop에서 ECB 없이 structural change 없음
- Native container가 system/world teardown에서 dispose됨
- `profile: game`이면 경계·baking 계약 변경 시 Architecture 갱신

## 출처

[wshobson/agents — unity-ecs-patterns](https://github.com/wshobson/agents/tree/main/plugins/game-development/skills/unity-ecs-patterns) (MIT, Copyright © 2024 Seth Hobson)에서 각색했어요. Kit 변경·고지: 저장소 [`NOTICE`](../../../NOTICE).
