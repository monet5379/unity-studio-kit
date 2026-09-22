# 에이전트 워크플로

personal · game 공통으로, 에이전트가 **어디까지 손대고 어떻게 최소로 고칠지**를 정해요. 프로필별 Plan·Architecture 무게는 personal / game 문서를 따르세요.

규칙: [`agent-scope.mdc`](../../.cursor/rules/common/agent-scope.mdc) · [`ponytail.mdc`](../../.cursor/rules/common/ponytail.mdc)

스킬(`.cursor/skills/`)은 **alwaysApply가 아니에요.** 리뷰·모듈 경계·아키텍처 스캔·DOTS·플레이어 빌드처럼 해당 요청이나 단계에서만 읽어요. 작은 수정은 포니테일만으로 충분해요.

리뷰(변경분) / 지금 구조 설명 / 리팩터 제안은 **한 요청에 섞지 않아요.** 세 가지를 한 번에 처리하는 것은 권장하지 않아요. 같이 오면 작업 전에 하나를 고르게 해요. 절차는 각 스킬 「의도를 섞지 않아요」.

## 스코프

- 변경 전 In Scope / Out of Scope를 확인해요.
- 요청과 **직접 관련된** 파일만 수정해요. 무관한 리팩터·포맷 일괄 변경은 금지예요.
- 명시 요청 없는 public API 시그니처 변경은 금지예요.
- `ThirdParty/` · `Plugins/` · 벤더 Assets는 **직접 수정하지 않아요** (어댑터만 프로젝트 코드에).

## 포니테일

이해한 뒤 **최소 diff**. YAGNI · 기존 헬퍼 재사용 · 표준 라이브러리 우선.  
비 trivial 로직 뒤에는 깨지면 실패하는 **실행 가능한 검증 하나**(작은 assert/테스트; 무거운 fixture 불필요)를 남겨요.

규칙 문구는 [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) Cursor 규칙을 한국어로 각색한 거예요 (MIT). 고지: [`NOTICE`](../../NOTICE).

## 검증

- 가능한 한 작은 단위로 진행해요.
- C# 변경 후 관련 asmdef 컴파일·수동 시나리오를 확인해요.
- 큰 구조 변경 시 프로젝트 문서(있으면 Architecture 등)를 같이 맞춰요. 문서 형식의 상세는 personal / game 프로필을 따르세요.

## 프로필

프로세스 무게·Plan·배포 규약은 `docs/personal/` · `docs/game/` (및 해당 `.cursor/rules`)에서 정해요.

Cursor 스킬: [`code-review`](../../.cursor/skills/code-review/SKILL.md) · [`codebase-design`](../../.cursor/skills/codebase-design/SKILL.md) · [`improve-codebase-architecture`](../../.cursor/skills/improve-codebase-architecture/SKILL.md) (호출 전용) · [`unity-ecs-patterns`](../../.cursor/skills/unity-ecs-patterns/SKILL.md) · [`unity-build-pipeline`](../../.cursor/skills/unity-build-pipeline/SKILL.md)
