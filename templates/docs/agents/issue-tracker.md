# 이슈 트래커

스펙·구현 티켓의 정본은 이 repo의 GitHub Issues이다. 절차는 Kit DevelopmentProcess (`unity-studio-kit/docs/game/DevelopmentProcess.md`)를 본다.

## 관례

- 스펙: 기능당 이슈 하나. 라벨 `spec`. 본문: Problem · Stories · Out of Scope · Implementation Decisions
- 티켓: 이슈 하나 (합본 금지). 라벨 `ticket`. 본문 첫 줄 `Parent: #<스펙 번호>`, acceptance, 의존은 `Blocked by: #<번호>`
- 상태: 라벨 ([triage-labels.md](triage-labels.md)). `done`은 라벨을 붙이고 이슈를 닫는다
- 경과: 이슈 코멘트
- 한 세션 실험: `.scratch/<feature-slug>/`. 이 경로에만 있으면 이슈를 만들지 않는다

## 스킬이 "publish to the issue tracker"라고 할 때

`gh issue create`로 이 repo에 만든다. 라벨이 없으면 `gh label create`로 triage 표의 이름을 만든다.

- 스펙: `--label spec`
- 티켓: `--label ticket`. 본문 첫 줄은 `Parent: #<스펙 번호>`

## 스킬이 "fetch the relevant ticket"라고 할 때

`gh issue view <번호> --comments`로 읽는다.

## 로컬 파일

override 표의 Issue tracker 모드가 `로컬 티켓만`일 때만 `docs/plan/tickets/<feature-slug>/` 아래 `spec.md`와 `issues/<NN>-<slug>.md`를 쓴다. 그 외에는 이 파일을 만들지 않는다.
