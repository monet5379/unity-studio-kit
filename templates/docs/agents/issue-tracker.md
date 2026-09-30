# 이슈 트래커

스펙·구현 티켓의 정본 경로예요. GitHub Issues가 아니에요. 절차는 Kit [DevelopmentProcess](../../../docs/game/DevelopmentProcess.md)를 보세요.

## 관례

- 기능당 디렉터리: `docs/plan/tickets/<feature-slug>/`
- 스펙: `docs/plan/tickets/<feature-slug>/spec.md`
- 구현 티켓: `docs/plan/tickets/<feature-slug>/issues/<NN>-<slug>.md` (`01`부터, 합본 금지)
- Triage: 티켓 상단 `Status:` ([triage-labels.md](triage-labels.md))
- 댓글: 파일 하단 `## Comments`

한 세션 실험만이면 `.scratch/<feature-slug>/`를 써요. 그때는 이 파일을 그 경로로 고치세요.

## 스킬이 "publish to the issue tracker"라고 할 때

`docs/plan/tickets/<feature-slug>/` 아래 파일을 만들어요. 디렉터리가 없으면 생성해요.

## 스킬이 "fetch the relevant ticket"라고 할 때

참조된 경로의 파일을 읽어요.

## GitHub

사용자가 명시하기 전에는 `gh issue create`로 스펙을 올리지 않아요.
