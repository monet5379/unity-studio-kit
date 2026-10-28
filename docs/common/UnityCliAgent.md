# Unity CLI · 에이전트

personal · game 공통으로, Unity **headless CLI**(`-batchmode`, `unity test`, `-executeMethod` 등)를 **에이전트 Shell에서 돌리지 않게** 한다. 검증·빌드·스모크는 저장소에 문서화된 **로컬 래퍼**를 사용자가 실행하고, 에이전트는 **명령 안내**와 **결과 로그 해석**만 한다.

에이전트 요약: [`.cursor/rules/common/unity-cli-agent.mdc`](../../.cursor/rules/common/unity-cli-agent.mdc)

## 한 줄

에이전트 Shell로 Unity Editor/CLI headless를 실행하지 않는다. 프로젝트 정본에 적힌 래퍼(Windows는 `.bat` 우선)를 채팅에 안내하고, 사용자가 로컬에서 실행한다.

## Must not (에이전트 Shell)

- `Unity.exe` · Hub Editor를 **`-batchmode`**, **`-nographics`**, **`-quit`**, **`-executeMethod`**, **`unity test`** 등으로 호출
- 위와 동일한 **`scripts/` · `tools/` 아래 PowerShell·shell 래퍼** 실행 (`.bat`는 보통 `.ps1`을 감싼 것 — 사용자 측 실행)
- headless 실패를 “에이전트가 Unity를 한 번 더 돌린다”로 해결하려는 시도
- 래퍼가 없을 때 임의 `Unity.exe` 경로·인자를 **만들어** Shell 실행

## Must

- 테스트·verify·플레이어 빌드·스모크가 필요하면 **실행하지 않고**, 프로젝트 `AGENTS.md` override · README · `scripts/README` · `Architecture_*`에 적힌 **진입점 한 줄**을 채팅에 제시한다.
- Windows에서 `.bat`와 `.ps1`을 둘 다 제공하면 안내는 **`.bat`를 우선**한다.
- 래퍼가 **없으면**(`AGENTS` override `—`) Unity **에디터**(Test Runner·문서화된 메뉴) 절차를 안내한다.
- 사용자가 exit code · `Logs/` · `logs/verify/` 등 **산출물**을 주면 그걸로 디버깅·문서 write-back한다.
- C# 변경 후 “확인”은 [AgentWorkflow.md](AgentWorkflow.md) §검증(코드·asmdef·인라인 assert)을 따르고, Unity batch로 컴파일·테스트를 **대체하지 않는다**.

## 예외

- 사용자가 채팅에서 **에이전트 Shell 실행을 명시 요청**한 경우

## 프로젝트 override (`AGENTS.md`)

| 항목 | 설명 |
|------|------|
| Unity CLI 진입점 | 예: `scripts/unity-test.bat`, `scripts/verify.ps1`, `—`(에디터만) |
| Unity CLI 정본 문서 | 예: `scripts/README.md`, `docs/.../Architecture_Testing.md` |

경로·레인·카테고리는 타이틀·패키지마다 다르다. Kit common은 **금지·안내 방식**만 고정한다.

## 관련

- Shell 삭제: [ShellSafety.md](ShellSafety.md) (별개)
- 스코프·검증: [AgentWorkflow.md](AgentWorkflow.md)
- game Verify·QA 제안: [DevelopmentProcess.md](../game/DevelopmentProcess.md) §Verify · [verification-qa-defaults.mdc](../../.cursor/rules/game/verification-qa-defaults.mdc)
- CI headless **패턴**(스크립트 작성): [unity-build-pipeline](../../.cursor/skills/unity-build-pipeline/SKILL.md) — 에이전트 Shell 실행은 이 페이지가 이김
