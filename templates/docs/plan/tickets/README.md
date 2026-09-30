# tickets

`/to-spec` · `/to-tickets` · `/implement`용 로컬 마크다운 트래커예요. 설계 정본과 Architecture를 대체하지 않아요.

트래커 조작: [`docs/agents/issue-tracker.md`](../../agents/issue-tracker.md). 운영 규칙은 Kit [DevelopmentProcess](../../../../docs/game/DevelopmentProcess.md)예요.

## Layout

```text
docs/plan/tickets/<feature-slug>/
  spec.md
  issues/
    01-<slug>.md
```

- 번호는 `01`부터. 상단에 `Blocked by: NN`.
- `00`은 사람 선행만. 뒤 티켓을 막지 않아요.
- `Status:`는 [`triage-labels`](../../agents/triage-labels.md).
- 대화·Play 결과는 `## Comments`.
- 남는 결정은 설계 정본 또는 `docs/adr/`로 돌려요.

## 이 타이틀에서 더할 것

Kit 표를 그대로 쓰지 않고, 여기에는 **이 게임만의 제약**만 적어요. 예: behavioral seam 씬 이름, 하루 끝 write-back 대상 문서.
