# Triage 라벨

스킬은 다섯 가지 triage 역할로 말한다. 로컬 마크다운에서는 GitHub 라벨 대신 티켓 상단 `Status:`에 오른쪽 열을 쓴다. 수명주기 값은 스킬 역할이 아니고, 아래 두 번째 표만 쓴다.

## Triage

| 스킬 역할 | 이 레포 `Status:` | 의미 |
|-----------|-------------------|------|
| `needs-triage` | `needs-triage` | 담당자가 이슈를 평가해야 함 |
| `needs-info` | `needs-info` | 제보자에게 추가 정보 대기 |
| `ready-for-agent` | `ready-for-agent` | 스펙이 충분해 에이전트가 진행 가능 |
| `ready-for-human` | `ready-for-human` | 사람이 구현해야 함 |
| `wontfix` | `wontfix` | 처리하지 않음 |

트래커 어휘가 다르면 **이 표의 오른쪽 열만** 고친다.

## 수명주기

티켓이 착수된 뒤의 `Status:`이다. 이 표는 프로젝트 말로 바꾸지 않는다. GDD 태그(`locked` 등)와 Architecture 본편 상태는 이 어휘와 다르다.

| `Status:` | 의미 |
|-----------|------|
| `in-progress` | 구현 중 |
| `done` | Verify를 통과하고, 구조가 바뀌었으면 Record까지 끝남 |

`resolved`, `Completed`, `superseded`는 쓰지 않는다. archive는 Status가 아니라 티켓 폴더를 치우는 동작이다.
