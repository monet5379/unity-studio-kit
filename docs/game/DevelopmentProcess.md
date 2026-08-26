# 개발 프로세스 (game · 7단계)

game 작업에서 **언제 무엇을 닫는지**를 공통 프레임으로 맞춰요. 산출물 무게는 규모에 비례하고, 핫픽스 Define은 대화 한 줄로도 돼요.

**왜 7단계인가요?** 구현만 반복하면 범위·구조·검증이 뒤섞여요. Define→Record로 “성공했는지 / 닫아도 되는지 / 실패 시 어디로 돌아갈지”를 같은 언어로 맞춰 둬요.

Cursor: [`development-process.mdc`](../../.cursor/rules/game/development-process.mdc) · [`verification-qa-defaults.mdc`](../../.cursor/rules/game/verification-qa-defaults.mdc)  
관련: [Documentation.md](Documentation.md) · [AgentWorkflow](../common/AgentWorkflow.md)

## 원칙

- 모든 작업은 Define → Design → DoD → Build → Verify → Record. 산출물은 규모에 비례해요 (핫픽스 Define = 대화 한 줄 OK).
- **Plan 파일**은 범위가 클 때만. 7단계 ≠ 매번 Plan 필수예요.
- common **ponytail**은 Build 스타일(최소 diff). 7단계를 생략하지 않아요.
- 실패 시 맹목 재시도 금지 → Recovery 분류 후 해당 단계로.

## 단계

| # | 단계 | 목적 |
|---|------|------|
| 1 | **Define** | 목표·Success Criteria·In/Out |
| 2 | **Design** | 구조·경계 변경 시에만 — Architecture · Plan (코드 수정안 없음) |
| 3 | **DoD** | PR·태스크 닫기 조건 (Tier·문서·`.meta` 등) |
| 4 | **Build** | 작은 단계 구현 |
| 5 | **Verify** | SC·Plan「확인」대조 |
| 6 | **Record** | 로그 · Architecture 반영 · Plan archive |
| 7 | **Recovery** | 실패 시에만 |

### Success Criteria

| 유형 | Verify |
|------|--------|
| **static** | 코드·문서·asmdef 리뷰 |
| **behavioral** | Plan「확인」·런타임 — **코드 리뷰만으로 pass 금지** |

### Verify vs QA 제안

- Verify(대조)는 항상 해요.
- 스모크·QA 러너·「테스트해보세요」**제안·실행**은 사용자 **명시 요청 전 금지**예요.
- Build 중 asmdef 컴파일 등 최소 기술 확인은 OK예요.

## Recovery

Build 재시도 전, 위에서 첫 yes:

| | 분류 | 조치 |
|---|------|------|
| 도메인·엔진 제약 누락? | 컨텍스트 | Architecture Gotchas · 규칙 1~3줄 |
| 범위 이탈? | 방향 | Define 재고정 · revert |
| Tier·폴더 위반? | 구조 | Design · 재배치 |
| 구현 버그만? | — | Build fix (Recovery 아님) |

조치 후 Record에 남겨요.
