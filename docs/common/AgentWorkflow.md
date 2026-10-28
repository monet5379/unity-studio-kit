# 에이전트 워크플로

personal · game 공통으로, 에이전트가 **어디까지 손대고 어떻게 최소로 고칠지**를 정한다. 
프로필별 Plan·Architecture 무게는 personal / game 문서를 따른다.

규칙: [`agent-scope.mdc`](../../.cursor/rules/common/agent-scope.mdc)

## 스코프

- 변경 전 In Scope / Out of Scope를 확인한다.
- 작업 전에 관련 타입·씬·프리팹·테스트를 조사한다.
- 요청과 **직접 관련된** 파일만 수정한다. 무관한 리팩터·포맷 일괄 변경은 금지다.
- 범위를 넓힐 때는 사용자 확인을 받거나, Plan에 확장 근거를 적는다.
- 큰 리팩터·구조 변경은 Plan과 구현을 나눠요. game 프로필·프로젝트 규칙이 Plan을 요구할 때이다.
- 명시 요청 없는 public API 시그니처 변경은 금지다.
- `ThirdParty/` · `Plugins/` · 벤더 Assets는 **직접 수정하지 않는다** (어댑터만 프로젝트 코드에).
- 다른 저장소의 공유 패키지 소스·캐시는 이 워크스페이스에서 수정하지 않는다. 소비 프로젝트는 manifest pin·호출 코드만 두고, 구현은 그 패키지 정본 repo에서 한다.

## 정본 우선순위

- 프로젝트 `AGENTS.md` override > Kit profile(personal / game) > Kit common. override는 AGENTS의 override 표에 적힌 값만 해당한다.
- 코드 > 프로젝트 정본 문서 (game: Architecture ≥ 설계 정본 · personal: Architecture ≥ README Invariants). game의 스킬·규칙 사다리는 [DevelopmentProcess](../game/DevelopmentProcess.md#스킬·규칙-우선순위).

## 포니테일

이해한 뒤 **최소 diff**. YAGNI · 기존 헬퍼 재사용 · 표준 라이브러리 우선.  
비 trivial 로직 뒤에는 깨지면 실패하는 **실행 가능한 검증 하나**(작은 assert/테스트; 무거운 fixture 불필요)를 남긴다.  
이 검증은 코드 안의 assert·작은 테스트이다. Play·스모크·QA 제안은 game이면 [DevelopmentProcess](../game/DevelopmentProcess.md) §Verify를 따른다.

에이전트용 전문은 Kit가 배포하지 않는다. 프로젝트 `.cursor/skills/ponytail/`(`/ponytail`)로 [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail)을 각색·설치한다 (MIT). 고지: [`NOTICE`](../../NOTICE).

## 검증

- 가능한 한 작은 단위로 진행한다.
- C# 변경 후 관련 asmdef가 컴파일되는지만 확인한다 (코드·리뷰 수준 — Unity batch로 대체하지 않음).
- Unity headless CLI는 에이전트 Shell에서 실행하지 않는다. [UnityCliAgent.md](UnityCliAgent.md).
- 비 trivial 로직의 인라인 검증(assert·작은 테스트)은 포니테일을 따른다.
- Play·스모크·QA 러너·「테스트해 보라」 제안은 프로필 규칙을 따른다. game은 DevelopmentProcess §Verify다.
- 큰 구조 변경 시 프로젝트 문서(있으면 Architecture 등)를 같이 맞춘다. 문서 형식의 상세는 personal / game 프로필을 따른다.

## 프로필

프로세스 무게·Plan·배포 규약은 `docs/personal/` · `docs/game/` (및 해당 `.cursor/rules`)에서 정한다.
