# 에이전트 워크플로

personal · game 공통으로, 에이전트가 **어디까지 손대고 어떻게 최소로 고칠지**를 정해요. 프로필별 Plan·Architecture 무게는 personal / game 문서를 따르세요.

규칙: [`agent-scope.mdc`](../../.cursor/rules/common/agent-scope.mdc) · [`ponytail.mdc`](../../.cursor/rules/common/ponytail.mdc)

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
