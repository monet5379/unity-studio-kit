---
name: codebase-design
description: >-
  깊은 모듈(작은 interface, 많은 구현) 설계 어휘. 모듈 interface·시임 위치,
  테스트하기 쉬운 경계, Design it twice, game Design 단계(코드 수정 없음),
  아키텍처 후보를 깊게 만들 때 사용.
---

# Codebase Design

**깊은 모듈:** 작은 interface 뒤에 많은 구현, 깨끗한 시임, 그 interface로 검증. 호출자에게는 leverage, 유지보수에는 locality.

이 스킬은 **설계 대화**용이에요. 작은 버그픽스·최소 diff를 이유로 추상화를 만들지 않아요. 포니테일이 이깁니다. DOTS 시스템 내부는 [`unity-ecs-patterns`](../unity-ecs-patterns/SKILL.md)가 이깁니다.

## 사용할 때

- 사용자가 모듈 경계·interface·시임 위치를 물어볼 때
- `profile: game` **Design** (구조·경계 변경, 코드 수정안 없음)
- [`improve-codebase-architecture`](../improve-codebase-architecture/SKILL.md)가 이 어휘를 필요로 할 때
- Design it twice로 여러 interface 안을 비교할 때

## 사용하지 않을 때

- 한 줄 버그픽스, 포니테일 최소 diff
- 요청 없는 `IFoo` / `IBarService` 추가
- MonoBehaviour·ECS 핫패스에 웹식 DI를 강제할 때
- DOTS `ISystem` / ECB / 쿼리 패턴 — `unity-ecs-patterns`

## 의도를 섞지 않아요

다음을 **한 요청에** 넣으면 이 스킬을 바로 돌리지 않아요. 작업 전에 어떤 의도인지 확인해요.

- 변경분 리뷰 (Standards / Spec) → [`code-review`](../code-review/SKILL.md)
- 지금 구조 설명 (as-is, 리팩터 없음) → Architecture / AGENTS / README. 전용 스킬 없음
- 리팩터 제안 (deepening 후보) → [`improve-codebase-architecture`](../improve-codebase-architecture/SKILL.md)

세 가지를 한 번에 처리하는 것은 **권장하지 않아요.** 검토+구조+리팩터가 한 문장이면 Design it twice를 시작하지 않아요. 사용자가 하나를 고를 때까지 대기해요. (고른 뒤 Design·시임만이면 이 스킬을 이어가요.)

```text
한 요청에 리뷰 / 구조 설명 / 리팩터 제안이 같이 있어요.
세 가지를 한 번에 하지 않는 것이 킷 권장이에요. 이번엔 어느 쪽인가요?

1. 고정점부터 diff 리뷰 (code-review)
2. 지금 구조만 설명 (리팩터 없음)
3. 아키텍처 후보만 (improve-codebase-architecture)
```

## 프로젝트 override (먼저 확인)

- `profile: game`: Architecture **Boundaries · Key Types · Invariants**가 이깁니다
- `profile: personal`: README Invariants가 이깁니다
- 샘플 타입명을 도메인 문서 없이 복사하지 마세요

## 어휘

설계 대화에서 아래 단어를 씁니다. **킷·Unity 단어를 지우지 않아요.** Architecture 섹션명 `Boundaries`, Unity `Component`, agent-scope의 **public API**는 그대로 둡니다.

| 설계 용어 | 이 Kit에서 |
|-----------|------------|
| **Module** | interface와 구현이 있는 단위. 기능 하나, asmdef, 클래스 묶음. Unity `Component`(MB/ECS)와 **다른 말** |
| **Interface** | 호출자가 올바르게 쓰려면 알아야 하는 전부 — 시그니처뿐 아니라 불변조건, 순서, 실패, 설정, 성능. C# `interface` / 킷 public API보다 넓음 |
| **Implementation** | 모듈 안쪽 코드. **Adapter**와 구분: 시임이 주제일 때만 adapter |
| **Depth** | interface 대비 호출자가 얻는 행위의 양. 작을수록 **shallow** |
| **Seam** | 그 자리를 안 고치고 행동을 바꿀 수 있는 위치. Architecture **Boundaries**와 대응 |
| **Adapter** | 시임을 채우는 구현. 킷: 벤더는 손대지 않고 **어댑터만 프로젝트에** |
| **Leverage** | 깊이가 호출자에게 주는 것. interface 하나, 호출 N곳 |
| **Locality** | 깊이가 유지보수에 주는 것. 변경·버그·검증이 한곳에 모임 |

**Shallow:** interface가 구현만큼 복잡함 (통과 래퍼). **Deep:** 작은 interface 뒤에 복잡한 구현.

interface를 고칠 때: 메서드를 줄일 수 있나, 인자를 단순화할 수 있나, 복잡도를 안으로 숨길 수 있나.

## 원칙

- 깊이는 **interface의 성질**이지 구현 줄 수가 아님. 모듈 안에 작은 내부 시임이 있어도 됨. 외부 interface로 열지 마세요
- **삭제 테스트.** 모듈을 지운다고 상상. 복잡도가 사라지면 통과 래퍼. N개 호출자에 다시 나타나면 제값을 함
- **interface가 테스트 표면.** 호출자와 테스트가 같은 시임을 넘어요. interface 너머를 테스트하고 싶으면 모듈 모양이 틀린 경우가 많아요
- **어댑터 하나 = 가설 시임, 둘 = 실재.** 실제로 갈리는 것이 없으면 시임을 만들지 않아요

## 테스트 가능성 (Unity 보정)

원 원칙 「의존성을 생성하지 마라 / 부수효과 말고 값을 반환하라」는 **순수 도메인 C#**에만 적용해요.

- `MonoBehaviour` 생명주기·물리·트랜스폼은 부수효과가 본업. 여기다 생성자 DI를 강제하지 않아요
- `GetComponent` 캐싱은 [`Csharp.md`](../../../docs/common/Csharp.md) hot path (`Awake` / `??=`)가 이깁니다
- 테스트용으로 시임을 여는 것은 프로덕션 어댑터 + 테스트 어댑터가 **둘**일 때만
- PlayMode·스모크·QA는 사용자 **명시 요청 전 제안하지 않아요**

## 상세

- 의존 분류·시임 규율: [references/deepening.md](references/deepening.md)
- 여러 interface 안 비교: [references/design-it-twice.md](references/design-it-twice.md)

설계·경계 작업이면 위 파일을 읽어요.

## 출처

[mattpocock/skills — codebase-design](https://github.com/mattpocock/skills/tree/HEAD/skills/engineering/codebase-design) (MIT, Copyright © 2026 Matt Pocock)에서 각색했어요. Kit는 용어 금지를 버리고 Unity·Architecture 단어를 병기하며, 의존 분류를 엔진에 맞췄어요. 고지: [`NOTICE`](../../../NOTICE).
