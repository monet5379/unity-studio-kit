# tickets

타이틀이 GitHub 티켓에 더하는 제약만 적는다. 스펙·티켓 본문은 이 repo의 GitHub Issues이다. 설계 정본과 Architecture를 대체하지 않는다.

트래커 조작: [`docs/agents/issue-tracker.md`](../../agents/issue-tracker.md). 운영 규칙은 Kit DevelopmentProcess (`unity-studio-kit/docs/game/DevelopmentProcess.md`)이다.

- 스펙은 라벨 `spec`. 티켓은 라벨 `ticket`, 본문 `Parent: #<스펙 번호>`.
- 의존은 `Blocked by: #<번호>`. `ready-for-human`은 뒤 티켓을 막지 않는다.
- 상태 라벨은 [`triage-labels`](../../agents/triage-labels.md).
- 대화·Play 결과는 이슈 코멘트.
- 남는 결정은 설계 정본 또는 `docs/adr/`로 돌린다.

## 이 타이틀에서 더할 것

Kit 표를 그대로 쓰지 않고, 여기에는 **이 게임만의 제약**만 적는다. 예: behavioral seam 씬 이름, 하루 끝 write-back 대상 문서, 스펙 이슈 번호.
