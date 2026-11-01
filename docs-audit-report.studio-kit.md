# unity-studio-kit 문서 진단 보고서

- 대상: `monet5379/unity-studio-kit` main `c843416` (2026-10-30 19:24 KST, "docs(writing): AI 초안 문체 규칙 추가"), 커밋 29개 (첫 커밋 2026-08-26 KST)
- 진단일: 2026-11-01 (KST). 읽기 전용. 저장소 쓰기·푸시·이슈 변경 없음. 폴더 생성 없음 (`/workspace` 아래 파일만 만듦)
- 기준: dragon 보고서(`/workspace/docs-audit-report.md`)와 같은 기준과 판정값. dragon 보고서는 수정하지 않았다.
- 표기: 근거는 `경로 L줄` 또는 `경로 §헤딩`. 근거가 없으면 `unknown`. 코드와 문서가 엇갈리면 어느 쪽이 옳은지 정하지 않고 `검증 필요`로 적는다.

## 0. 요약

- **문서 수:** md 33개 (참조 10 · 프로세스 6 · template 5 · entry(허브 포함) 5 · 개념 3 · skill 4)와 Cursor 규칙 `.mdc` 20개. 그 밖에 `NOTICE`·`LICENSE`·`.gitignore`가 있다.
- **상태 unknown 비율:** md 33/33 (100%). Kit 문서에는 `상태:`/`Status:` 표기가 하나도 없다. Kit는 정본 모음이라 생애주기 상태가 덜 중요하지만, "현행 정본인지"를 표시하는 수단이 없다.
- **진입 문서:** Kit 저장소 루트에는 `AGENTS.md`가 없다. 진입은 `README.md`(88줄, 길이 적정)와 alwaysApply 규칙 4개, 소비 repo용 `templates/AGENTS.game.md`(100줄)이다. README에 옛 라벨이 2곳 있다(L57·L61).
- **정본 적합성 판정: 개선 필요.** 탐색 규칙(프로필 층·정본 우선순위·위키 계약·결정 트리)과 금지 규칙(.meta·Shell·Unity CLI)은 잘 갖췄다. 그러나 ① 완료 계열 Status 어휘가 없고, ② DoD 정의가 "ready-for-agent"로 모호하며, ③ 작업 유형별 읽기 규칙이 없고, ④ `/tdd`·seam 테스트와 "에이전트 CLI 금지"가 같은 Kit 안에서 맞물리지 않는다. 템플릿의 깨진 링크와 옛 라벨은 복사될 때마다 소비 repo로 퍼진다(dragon AGENTS L136에 실제로 복제됨).
- **dragon과의 관계:** dragon의 대표 충돌(커밋 제목 이슈 번호 필수, GitHub 이슈 쌍 필수, `.cursor/skills/matt-pocock/` 경로, 결정 트리 SSOT 이중 선언, Notion을 정본 사다리 2순위에 둠)은 Kit가 허용한 override 범위 밖이거나 override 표에 적히지 않았다. 한편 dragon 보고서의 일부 판정은 Kit를 보고 다시 봐야 한다(§3.4).

## 1. 문서 목록

판정 방법
- 유형: Kit 허브 README 표의 `유형` 열(`docs/common/README.md`·`docs/game/README.md`·`docs/personal/README.md`)을 그대로 썼다. 루트·허브 README는 entry, `templates/`는 template, `.cursor/skills/`는 skill이다.
- 상태: 파일 상단에 상태 표기가 없으면 `unknown (표기 없음)`. 33개 모두 해당한다.
- 줄 수: raw 본문 기준. ±1 오차가 있을 수 있다. entry 150줄 초과 `김`, 300줄 초과 `매우 김`(해당 없음). 일반 문서 500줄 초과 `분리 검토`(`unity-ecs-patterns/references/details.md` 585줄 1건).
- 마지막 수정: 그 파일을 건드린 가장 최근 커밋의 시각을 KST로 바꿨다. 최신성 기준선은 30일(2026-10-02 KST 이전이면 30일 초과). md 33개는 모두 30일 이내이다. Kit에는 대응 코드가 없어서, "코드 이후 변경" 대신 **삭제·이동된 항목을 가리키는 옛 라벨**이 있으면 `높음`으로 적었다.
- 중복·충돌 ID(K*, KC*)는 §4에 정리했다.

### 1.1 md 문서 (33)

| 경로 | 유형 | 상태 | 주제 | 줄 수 | 마지막 수정 (KST) | 최신성 위험 | 중복·충돌 | 권장 조치 |
|---|---|---|---|---|---|---|---|---|
| `README.md` | entry | unknown (표기 없음) | Kit 소개·프로필·시작하기·구조 | 88 | 2026-10-30 19:24 | 높음 (L57 스킬 라벨·L61 포니테일 alwaysApply 옛 설명) | K5·K6 | 옛 라벨 수정 |
| `docs/common/README.md` | entry(허브) | unknown (표기 없음) | common 문서 목차·적용 시점 | 20 | 2026-10-30 19:24 | unknown (30일 이내) | — | 유지 |
| `docs/common/AgentWorkflow.md` | 프로세스 | unknown (표기 없음) | 스코프·정본 우선순위·포니테일·검증 | 43 | 2026-10-28 22:18 | unknown (30일 이내) | K2·K3, 해요체 L14 | 문체 1줄 수정 |
| `docs/common/CommitMessages.md` | 참조 | unknown (표기 없음) | 커밋 형식·type·본문·프로젝트 override | 179 | 2026-10-18 12:08 | unknown (30일 이내) | K1 (UnityBasics·mdc·템플릿과 중복), L153 오탈자 | 이슈 번호·revert 정책 명시(§3.3) |
| `docs/common/Csharp.md` | 참조 | unknown (표기 없음) | C# 네이밍·프로퍼티·partial·hot path | 68 | 2026-10-18 20:39 | unknown (30일 이내) | csharp-standards.mdc·naming-semantics.mdc 요약(의도된 이원화), L53 오탈자 | 오탈자 수정 |
| `docs/common/DevImgui.md` | 참조 | unknown (표기 없음) | 개발용 IMGUI 스타일 (선택) | 37 | 2026-10-18 12:08 | unknown (30일 이내) | DemoGui.md와 역할 분담, L29 오탈자 | 오탈자 수정 |
| `docs/common/RulesEvaluationScorecard.md` | 프로세스 | unknown (표기 없음) | 규칙 평가 스코어카드 (빈 양식) | 168 | 2026-10-28 22:18 | unknown (30일 이내) | §7.4 ↔ 템플릿 L78 링크(KC4), L6 오탈자 | 유지 (첫 평가 기록 권장) |
| `docs/common/ShellSafety.md` | 참조 | unknown (표기 없음) | Shell 삭제 안전 | 82 | 2026-10-18 12:08 | unknown (30일 이내) | shell-destructive-ops.mdc 요약(의도된 이원화) | 유지 |
| `docs/common/UnityBasics.md` | 참조 | unknown (표기 없음) | .meta·씬 YAML·워크스페이스·커밋 | 40 | 2026-10-28 22:18 | unknown (30일 이내) | K1 (§Git / 커밋이 CommitMessages와 중복) | 커밋 절을 링크 1줄로 축소 |
| `docs/common/UnityCliAgent.md` | 참조 | unknown (표기 없음) | Unity headless CLI 에이전트 금지·래퍼 안내 | 44 | 2026-10-28 22:18 | unknown (30일 이내) | K3 ↔ DevelopmentProcess L129 `/tdd` seam 테스트(KC1) | 테스트 실행 주체 문장 추가 |
| `docs/common/WritingGuide.md` | 프로세스 | unknown (표기 없음) | 글쓰기·한다체·AI 초안·정본 사다리 | 203 | 2026-10-30 19:24 | unknown (30일 이내) | K2 (§정본 사다리), 오탈자 L32·L41·L53·L60 | 오탈자 수정 |
| `docs/game/README.md` | entry(허브) | unknown (표기 없음) | game 문서 목차 | 15 | 2026-10-18 20:39 | unknown (30일 이내) | — | `적용` 열 추가 (common/personal과 형식 통일) |
| `docs/game/Overview.md` | 개념 | unknown (표기 없음) | game 프로필 선택 기준 | 44 | 2026-10-25 14:55 | unknown (30일 이내) | L35 오탈자 | 오탈자 수정 |
| `docs/game/AssetsLayout.md` | 참조 | unknown (표기 없음) | Assets 폴더 배치·데이터 3층 | 58 | 2026-10-18 12:08 | unknown (30일 이내) | unity-assets-layout.mdc 요약 | 유지 |
| `docs/game/ProjectSeparation.md` | 개념 | unknown (표기 없음) | Core·Game·Editor asmdef 경계 | 60 | 2026-10-18 12:08 | unknown (30일 이내) | L28 해요체·L29 오탈자 | 문체 수정 |
| `docs/game/Documentation.md` | 참조 | unknown (표기 없음) | 문서 2분류·Architecture 골격·ADR·README 허브·위키 계약 | 241 | 2026-10-18 12:38 | unknown (30일 이내) | KC5 (L105 목적 이탤릭 vs 골격 L114~ 고정 문구), 합니다체 6줄 | 이탤릭 규칙 명확화·문체 수정 |
| `docs/game/DevelopmentProcess.md` | 프로세스 | unknown (표기 없음) | 스킬 체인·Issue tracker·Verify·Record·Recovery·닫기 어휘 | 132 | 2026-10-25 14:55 | unknown (30일 이내) | KC1·KC2·KC3, K2 | DoD·Status·테스트 실행 주체 정리 (P0) |
| `docs/personal/README.md` | entry(허브) | unknown (표기 없음) | personal 문서 목차 | 18 | 2026-10-18 12:38 | unknown (30일 이내) | — | 유지 |
| `docs/personal/Overview.md` | 개념 | unknown (표기 없음) | personal 프로필 선택 기준 | 44 | 2026-10-25 14:55 | unknown (30일 이내) | — | 유지 |
| `docs/personal/PackageLayout.md` | 참조 | unknown (표기 없음) | 복사형 패키지·Demo 레이아웃 | 34 | 2026-10-18 12:08 | unknown (30일 이내) | L21 오탈자("밝혀 주한다") | 오탈자 수정 |
| `docs/personal/DocsLite.md` | 프로세스 | unknown (표기 없음) | README 계약 + Architecture | 45 | 2026-10-18 12:38 | unknown (30일 이내) | game Documentation 골격 참조(의도) | 유지 |
| `docs/personal/LocaleDocs.md` | 프로세스 | unknown (표기 없음) | README 한글 단일 규칙 | 40 | 2026-10-18 12:38 | unknown (30일 이내) | L7 해요체("다뤄요") | 문체 수정 |
| `docs/personal/DemoGui.md` | 참조 | unknown (표기 없음) | Demo/F1 IMGUI (선택) | 70 | 2026-10-18 12:08 | unknown (30일 이내) | L69 타이틀명(Dragon) 언급, 오탈자 L36·L39·L63 | 오탈자 수정 |
| `.cursor/skills/unity-build-pipeline/SKILL.md` | skill | unknown (표기 없음) | 플레이어 빌드·IL2CPP·CI | 127 | 2026-10-28 22:18 | unknown (30일 이내) | L35 CLI 금지와 정합, L14 합니다체 | 유지 |
| `.cursor/skills/unity-build-pipeline/references/ci-build-script.md` | skill(참조) | unknown (표기 없음) | CI 빌드 스크립트 예시 | 113 | 2026-10-18 12:08 | unknown (30일 이내) | L92 오탈자 | 유지 |
| `.cursor/skills/unity-ecs-patterns/SKILL.md` | skill | unknown (표기 없음) | DOTS·ECS 패턴 | 96 | 2026-10-18 12:08 | unknown (30일 이내) | — | 유지 |
| `.cursor/skills/unity-ecs-patterns/references/details.md` | skill(참조) | unknown (표기 없음) | ECS 상세 예시 | 585 (분리 검토) | 2026-10-18 12:08 | unknown (30일 이내) | 585줄 → 분리 검토 | 분리 검토 (P2) |
| `templates/README.md` | entry(허브) | unknown (표기 없음) | 템플릿 사용법 | 20 | 2026-10-18 12:08 | unknown (30일 이내) | — | 유지 |
| `templates/AGENTS.game.md` | template | unknown (표기 없음) | game 타이틀 AGENTS 뼈대 | 100 | 2026-10-28 22:18 | 높음 (L54 "Kit common … 포니테일" 옛 라벨) | K1·K5·KC4 (L78 깨진 링크), L7 오탈자 | DoD·작업 유형별 읽기·Status 행 추가 (P0) |
| `templates/AGENTS.personal.md` | template | unknown (표기 없음) | personal 프로젝트 AGENTS 뼈대 | 67 | 2026-10-28 22:18 | unknown (30일 이내) | KC4 (L46 깨진 링크), L7 오탈자 | 링크→텍스트 경로 |
| `templates/docs/agents/issue-tracker.md` | template | unknown (표기 없음) | 티켓 트래커 정본 경로 | 25 | 2026-10-18 12:17 | unknown (30일 이내) | L13 오탈자 | 유지 |
| `templates/docs/agents/triage-labels.md` | template | unknown (표기 없음) | triage Status 5종 | 13 | 2026-10-18 12:08 | unknown (30일 이내) | KC2 (완료·진행 상태 없음), L13 오탈자 | 완료 계열 Status 추가 (P0) |
| `templates/docs/plan/tickets/README.md` | template | unknown (표기 없음) | 티켓 폴더 레이아웃 | 24 | 2026-10-18 12:17 | unknown (30일 이내) | — | 유지 |
### 1.2 Cursor 규칙 `.mdc` (20)

| 경로 (`.cursor/rules/` 아래) | 적용 방식 (frontmatter) | 줄 수 | 마지막 수정 (KST) | 최신성 | 비고 |
|---|---|---|---|---|---|
| `common/agent-scope.mdc` | alwaysApply | 43 | 2026-10-28 22:18 | 30일 이내 | L38 §포니테일 링크는 존재. L20 앵커 `#스킬·규칙-우선순위` 깨짐 의심 |
| `common/commit-messages.mdc` | alwaysApply: false, globs 없음 | 26 | 2026-10-10 12:53 | 30일 이내 | K1. 커밋 시점에 붙는지 검증 필요 |
| `common/csharp-standards.mdc` | glob `**/*.cs` | 66 | 2026-10-18 20:39 | 30일 이내 | — |
| `common/dev-imgui.mdc` | glob `**/*{GUI,Gui,Overlay}*.cs` | 29 | 2026-08-27 00:49 | 30일 초과 | — |
| `common/naming-semantics.mdc` | glob `**/*.cs` | 31 | 2026-09-30 15:07 | 30일 초과 (merge 커밋 기준, 실제 내용 변경일 unknown) | — |
| `common/shell-destructive-ops.mdc` | alwaysApply | 28 | 2026-09-30 15:07 | 30일 초과 (merge 커밋 기준, 실제 내용 변경일 unknown) | — |
| `common/unity-basics.mdc` | alwaysApply | 48 | 2026-10-28 22:18 | 30일 이내 | K1 (§Git / Commit 중복) |
| `common/unity-cli-agent.mdc` | alwaysApply | 24 | 2026-10-28 22:18 | 30일 이내 | K3 |
| `common/writing-guide.mdc` | glob docs·AGENTS·templates | 40 | 2026-10-30 19:24 | 30일 이내 | — |
| `game/agent-scope-game.mdc` | alwaysApply: false, globs 없음 | 25 | 2026-10-18 12:08 | 30일 이내 | L8 오탈자("얹다") |
| `game/development-process.mdc` | alwaysApply: false, globs 없음 | 51 | 2026-10-25 14:55 | 30일 이내 | KC1·KC2 요약본 |
| `game/documentation.mdc` | glob `**/docs/**/*.md` | 63 | 2026-10-18 12:38 | 30일 이내 | — |
| `game/game-profile.mdc` | alwaysApply: false, globs 없음 | 26 | 2026-10-18 12:08 | 30일 이내 | K5 (L13 "common(포니테일…)") |
| `game/unity-assets-layout.mdc` | glob `**/Assets/**` | 42 | 2026-10-18 12:08 | 30일 이내 | — |
| `game/verification-qa-defaults.mdc` | alwaysApply: false, globs 없음 | 34 | 2026-10-28 22:18 | 30일 이내 | KC3 (L20 ↔ DevelopmentProcess Plan「확인」) |
| `personal/demo-gui.mdc` | glob `**/Demo/**/*.cs` | 31 | 2026-10-18 12:08 | 30일 이내 | L30 타이틀명(Dragon) 언급 |
| `personal/documentation.mdc` | glob docs·README | 33 | 2026-10-18 12:38 | 30일 이내 | L33 깨진 링크 `../game/Documentation.md#readme-허브` |
| `personal/locale-docs.mdc` | alwaysApply: false, globs 없음 | 23 | 2026-10-18 12:38 | 30일 이내 | — |
| `personal/package-layout.mdc` | glob `**/Assets/**` | 23 | 2026-10-18 12:08 | 30일 이내 | — |
| `personal/personal-profile.mdc` | alwaysApply: false, globs 없음 | 34 | 2026-10-18 12:38 | 30일 이내 | K5 (L13) |
- alwaysApply는 4개(`agent-scope`·`shell-destructive-ops`·`unity-basics`·`unity-cli-agent`)이다. README L61은 "기본·스코프·포니테일·Shell·Unity CLI"가 alwaysApply라고 적었다. 포니테일 규칙은 0788460(2026-10-25 14:55 KST)에서 Kit에서 빠졌으므로 이 설명은 낡았다.
- game·personal 프로필 규칙 중 6개(`agent-scope-game`·`development-process`·`game-profile`·`verification-qa-defaults`·`locale-docs`·`personal-profile`)와 common `commit-messages`는 `alwaysApply: false`이고 globs도 없다. 이런 규칙은 에이전트가 description을 보고 고를 때만 붙는다(Cursor의 "Agent Requested" 동작으로 이해하지만, 이 진단에서 실제 동작은 관찰하지 못했다 → **검증 필요**). README L62 "profile:에 맞는 것만 따른다"를 강제하는 장치는 없다. 특히 "요청 전 QA·스모크 제안 금지"(`verification-qa-defaults.mdc`)가 로드되지 않을 수 있다.
- 멀티 루트의 두 번째 루트(Kit)에 있는 `.cursor/rules`를 Cursor가 실제로 읽는지도 이 진단 범위에서는 확인할 수 없다 → **검증 필요** (`RulesEvaluationScorecard.md` §1 배선·진입이 바로 이 점검 항목이다).

## 2. 진입 문서 진단

### 2.1 무엇이 진입점인가

| 진입점 | 줄 수 | 역할 | 근거 |
|---|---|---|---|
| `README.md` | 88 | Kit 소개, 프로필 고르기, 시작하기(템플릿 복사 → 멀티 루트), 구조, 스킬 표, 라이선스 | `README.md` §이 Kit로 하는 일 / 안 하는 일 · §프로필 고르기 · §시작하기 · §구조 |
| alwaysApply 규칙 4개 | 24~48 | 에이전트가 항상 받는 최소 규칙 (스코프·Shell·.meta·Unity CLI) | §1.2 frontmatter |
| `templates/AGENTS.game.md` · `AGENTS.personal.md` | 100 · 67 | 소비 repo 루트 `AGENTS.md`의 뼈대. 실제 프로젝트 에이전트의 진입점이 된다 | `README.md` L37 |
| 허브 README 3개 + `templates/README.md` | 15~20 | 폴더 목차 | 각 파일 |
| Kit 저장소용 `AGENTS.md` | 없음 | Kit 자체를 고칠 때의 에이전트 진입 문서가 없다. `game/documentation.mdc` L12·`unity-assets-layout.mdc` L11이 "Kit 저장소를 고칠 때"를 따로 다룰 뿐이다 | Kit tree (루트에 `AGENTS.md` 없음) |

### 2.2 길이·중복

- `README.md` 88줄, 템플릿 100줄로 모두 entry 기준 150줄 이하이다. 과밀하지 않다.
- README는 상세 규칙을 복제하지 않고 docs로 링크한다. 다만 §구조 아래 L61~62와 스킬 표 L71·L75~77에 규칙 요지가 있고, 그중 2곳이 낡았다(§4.3).
- `templates/AGENTS.game.md`는 Kit 규칙을 요약 한 줄과 텍스트 경로로 가리킨다(L9~13·L32·L45·L50). `docs/game/Documentation.md` L9("타이틀 AGENTS.md에는 요약 한 줄과 링크")와 맞다.

### 2.3 필수 요소 체크

| 요소 | Kit에 있는가 | 근거 | 템플릿(`AGENTS.game.md`)에 있는가 |
|---|---|---|---|
| 탐색 규칙 (무엇을 어디서 읽나) | 있음 — 프로필 층, 위키 계약(관련 Architecture(+GDD)만 읽기), 결정 트리(쓸 위치) | `README.md` §프로필 고르기 · `docs/game/Documentation.md` §에이전트 위키 계약 L11~22 · §어디에 쓸지 (결정 트리) L47 | Kit 경로 표만 (L9~13) |
| 작업 유형별 읽기 규칙 (버그·리팩터·밸런스·신규 설계별 문서 세트) | **없음**. common README의 `적용` 열(“커밋 시”, “C# 작성·수정 시”)이 가장 가깝다. game README에는 `적용` 열도 없다 | `docs/common/README.md` 표 · `docs/game/README.md` 표 | 없음 |
| 정본 우선순위 | 있음 | `docs/common/AgentWorkflow.md` §정본 우선순위 L19~22 · `docs/game/DevelopmentProcess.md` §스킬·규칙 우선순위 L28~38 | 없음 (L59 "표에 없는 값은 Kit를 따른다"만) |
| 코드 vs 문서 우선 | 있음 — 코드 ≥ Architecture ≥ 설계 정본 | `docs/game/Documentation.md` L22·L196~199 · `docs/common/WritingGuide.md` §정본 사다리 | 없음 |
| 코딩 규칙 | 있음 | `docs/common/Csharp.md` · `csharp-standards.mdc` · `naming-semantics.mdc` | L52 §코딩 (요약) |
| 금지 사항 | 있음 — .meta·GUID·Editor Setup·Shell 삭제·Unity CLI·ThirdParty | `docs/common/UnityBasics.md` · `ShellSafety.md` · `UnityCliAgent.md` | L36 §Unity / 에셋 |
| 검증 방법 | 있음 — asmdef 컴파일 확인, static/behavioral, QA 제안 금지 | `docs/common/AgentWorkflow.md` §검증 L32~38 · `docs/game/DevelopmentProcess.md` §Verify L95~104 | L45~48 (요약) |
| DoD (완료 정의) | **모호** — 닫기 어휘 표의 DoD 행은 닫힘을 `Status: ready-for-agent`로 적는다(L128). 같은 문서 §닫기 L93의 "작업 완료 = Verify (+Record)"와 뜻이 다르다. DoD가 "착수 준비 완료"인지 "작업 완료"인지 정해지지 않았다 | `docs/game/DevelopmentProcess.md` L93 · L128 | **없음** |
| Status 어휘 | **부분** — triage 5종(`needs-triage`·`needs-info`·`ready-for-agent`·`ready-for-human`·`wontfix`)만 있다. 진행 중·완료·폐기 상태가 없다. Record 행 L131의 "archive 또는 Completed"는 어디에도 정의되지 않은 값이다 | `templates/docs/agents/triage-labels.md` · `docs/game/DevelopmentProcess.md` L131 | 없음 |

판정 (dragon과 같은 척도): 진입 문서 자체는 짧고 탐색 규칙이 있어 **양호**에 가깝다. 하지만 DoD·Status·작업 유형별 읽기 규칙이 Kit에 없거나 모호하고, 템플릿도 이를 싣지 않는다. 그래서 소비 repo가 각자 만들게 되고(dragon의 C4 Status 4종 혼재), Kit 전체 판정은 **개선 필요**이다.

## 3. 규칙 정본으로서의 적합성

### 3.1 Kit 규칙 목록

| # | 규칙 | Kit 정본 (근거) | 요약 규칙(.mdc) | 소비 repo가 바꿀 수 있는 범위 |
|---|---|---|---|---|
| R1 | 커밋 형식 `<type>(<scope>): <제목>`, 한글 기본, 본문(why) 필수, type 8종(feat·fix·docs·style·refactor·perf·test·chore), 사용자 명시 요청 시에만 커밋 | `docs/common/CommitMessages.md` §형식 L11 · §Type L28 · §본문 · Footer L83 | `commit-messages.mdc` L10~26 | scope 목록·언어·패치노트 경로만 (L4·L165). "형식·type·작성법은 Kit" |
| R2 | 이슈 참조 | `CommitMessages.md` L91 "이슈 닫기는 footer 예: `Closes #12`" (예시뿐) | 없음 | **정해지지 않음** — 제목에 이슈 번호를 넣는 규칙도, 금지도 없다 |
| R3 | Unity headless CLI를 에이전트 Shell에서 실행 금지, `scripts/`·`tools/` 래퍼 실행도 금지, 진입점 한 줄만 안내(.bat 우선), 사용자 명시 요청이 유일한 예외 | `docs/common/UnityCliAgent.md` L3·L13 | `unity-cli-agent.mdc` L10~24 (alwaysApply) | 진입점·정본 문서 경로 (템플릿 override 표 L78~79) |
| R4 | 검증 = 관련 asmdef 컴파일 확인. static/behavioral 구분. 스모크·QA는 요청 전 제안·실행 금지 | `docs/common/AgentWorkflow.md` §검증 L32~38 · `docs/game/DevelopmentProcess.md` §Verify L95~104 | `agent-scope.mdc` L37 · `verification-qa-defaults.mdc` | behavioral seam(어떤 씬 Play인지)은 타이틀 AGENTS (DevelopmentProcess L82) |
| R5 | 테스트 작성 | `DevelopmentProcess.md` L20·L22 (`/tdd` seam) · L82 "새 유닛 테스트 seam은 합의 없이 열지 않는다" · L129 "diff와 seam 테스트" | `development-process.mdc` | **테스트 실행 주체가 정해지지 않음** (KC1) |
| R6 | 정본 우선순위: 프로젝트 AGENTS override > Kit profile > Kit common. override는 AGENTS override 표에 적힌 값만 | `AgentWorkflow.md` §정본 우선순위 L21 · `agent-scope.mdc` L19 | 동일 | — |
| R7 | 코드 vs 문서: 코드 ≥ Architecture ≥ 설계 정본(GDD `locked`·Technical Design). 외부 PDF·브리프는 확인용 | `docs/game/Documentation.md` L22·L196~199 · `WritingGuide.md` §정본 사다리 | `documentation.mdc` L31 | — |
| R8 | 스킬·규칙 우선순위: 타이틀 AGENTS > 타이틀 오버레이 > 타이틀 `.agents/skills/` > Kit game > Kit common. Matt 스킬은 타이틀 `.agents/skills/`가 정본 | `DevelopmentProcess.md` §스킬·규칙 우선순위 L28~38 · `README.md` L71 | `development-process.mdc` L24 | — |
| R9 | Issue tracker: GitHub Issues 필수 아님, 명시 전 `gh issue create` 금지. 임시 `.scratch/`·추적 `docs/plan/tickets/` | `DevelopmentProcess.md` §Issue tracker L40~65 | `development-process.mdc` L26~31 | 경로 (템플릿 override 표 L71 "Issue tracker" 행) |
| R10 | 문서 Status 어휘: triage 5종 | `templates/docs/agents/triage-labels.md` | 없음 | "오른쪽 열만" 바꿀 수 있음 (L13) |
| R11 | DoD | `DevelopmentProcess.md` §닫기 L88~93 · §닫기 어휘 L128 | `development-process.mdc` §닫기 | — (모호, §2.3) |
| R12 | 문서 2분류·Architecture 골격(소제목 아래 목적 이탤릭 한 줄)·250줄 검토 신호·README 허브(bare `UI.md`/`Combat.md` 금지)·GDD 태그 5종·enum 전체 복사 금지 | `docs/game/Documentation.md` §Architecture 작성 규약 L100~161 · §README 허브 L221~225 · §GDD를 쓸 때 L201 | `documentation.mdc` | 경로(문서 루트·GDD 경로) |
| R13 | 규칙 본문은 Kit 문서에만. `.mdc`·타이틀 AGENTS에는 요약 한 줄 + 링크 | `docs/game/Documentation.md` L9 · `WritingGuide.md` §docs와 rules L44~53 | `writing-guide.mdc` L16 | — |
| R14 | 글쓰기: 한다체, lead, 한 페이지 한 주제, 제목 부제(—) 금지. 적용 대상에 game 타이틀 `docs/`·`AGENTS.md` 포함. 톤 예외는 AGENTS가 지정한 `notes/`·`interview/` | `WritingGuide.md` §적용 범위 L11 · §독자 · 톤 L16 · L61 | `writing-guide.mdc` L15~18 | 톤 예외 경로 |
| R15 | Assets 배치: `Assets/Project/`, `Addressables/`(복수), `Resources/`는 브리지, 공유 Core는 UPM, 레거시 `Assets/Scripts/`에 신규 기능 금지 | `docs/game/AssetsLayout.md` · `ProjectSeparation.md` | `unity-assets-layout.mdc` L13~42 | 경로 (override 표) |
| R16 | .meta·GUID·Editor Setup 배선 금지, Shell 삭제 절차, C# 네이밍·`init` 금지·코드 주석 금지 | `UnityBasics.md` · `ShellSafety.md` · `Csharp.md` | alwaysApply 3개 + glob 2개 | 도메인 delta rule (`naming-semantics.mdc` L27) · const 등 override 표 |
| R17 | Kit 참조 방식: 텍스트 경로 `unity-studio-kit/...`, 드라이브 루트를 거치는 상대 링크 금지 | `docs/common/RulesEvaluationScorecard.md` §7 L144 (7.4) | 없음 | — (평가 항목으로만 존재) |

### 3.2 dragon-is-dead와 대조

대조 대상: `/workspace/mirror` (dragon main `340e742` 미러). 

| 항목 | Kit 규칙 | dragon 현황 (근거) | 판정 |
|---|---|---|---|
| **커밋 — 이슈 번호 필수** | R1·R2: 프로젝트가 정할 수 있는 것은 scope·언어·패치노트뿐. 이슈 참조는 footer 예시(`Closes #12`) | `GIT_CONVENTIONS.md` §이슈 번호 규칙 L119~: 제목 끝 ` (#번호)`, feat·fix·refactor **필수** | **충돌 (Kit override 범위 밖).** 제목 형식을 바꾸는 규칙인데 `AGENTS.md` §이 타이틀 override(L120)에도, §Git 커밋 메시지(L88)에도 없다 |
| 커밋 — 정본 위치 | R1·R6: 형식은 Kit, 프로젝트 값은 AGENTS | `AGENTS.md` L88~ "Kit CommitMessages를 따릅니다" vs `GIT_CONVENTIONS.md` L3 "이 문서가 커밋 규칙의 정본" | **충돌.** 정본이 셋(Kit·AGENTS·GIT_CONVENTIONS)이다. dragon 보고서 C1(순환)과 같은 문제를 Kit 기준으로 보면 "Kit + AGENTS 커밋 표"로 접어야 한다 |
| 커밋 — type | R1: 8종, `revert` 없음 | `AGENTS.md` L101: `revert` 추가, `style` 빠짐 | **경미한 충돌.** Kit는 type 목록 override를 허용하지 않는다. Kit에 `revert` 정책이 없는 것도 원인 |
| **테스트 실행** | R3·R4: 에이전트는 실행 금지, 래퍼는 안내만 | `AGENTS.md` L58: 요청 없이 실행 금지 → 일치. 단 L58은 `scripts/unity-test*.ps1`, override 표 L136은 `scripts/*.bat` (Kit는 .bat 우선) | 대체로 일치. ps1/bat 표기 불일치는 경미 |
| 테스트 — 스킬 | R3 vs R5 | `.cursor/skills/matt-pocock/implement/SKILL.md` L27 "run focused EditMode tests … compile + tests are the gate" | **충돌** (dragon C5). 원인 일부는 Kit에 있다: Kit도 `/implement`·`/tdd` seam 테스트(L22·L129)를 요구하면서 누가 돌리는지 정하지 않았다(KC1) |
| **AGENTS → Kit 연결** | README §시작하기, 템플릿 L4·L9~13, R17 텍스트 경로 | `AGENTS.md` L4 `profile: game` 있음. L12~18 Kit 표는 템플릿 L9~13을 그대로 복사했다. 텍스트 경로 사용 → R17과 일치 | **일치.** 단 L136의 `[UnityCliAgent](unity-studio-kit/docs/common/UnityCliAgent.md)`는 markdown 링크라 dragon repo 안에서 깨진다. 템플릿 L78에서 그대로 복제된 것이다(KC4) |
| Kit 규칙 로드 | §1.2 | `AGENTS.md` L200 "Kit common/game rules는 멀티 루트 Kit에서 읽습니다" | **검증 필요** — 두 번째 루트의 `.cursor/rules` 로드, globs 없는 프로필 규칙의 적용 여부는 관찰하지 못함 |
| **Issue tracker** | R9: GitHub 필수 아님, 명시 전 `gh issue create` 금지. 템플릿 L59 "Kit와 다른 값은 반드시 이 표에" | `AGENTS.md` §Issue tracker L219~221: 새 work item은 로컬 티켓과 GitHub 이슈 **쌍** 필수. override 표(L120~)에 Issue tracker 행이 없다 | **충돌 (override 표 누락).** R6에 따르면 AGENTS override가 이기지만 "표에 적힌 값만"이라는 조건을 못 채운다 |
| 스킬 위치 | R8: 타이틀 `.agents/skills/` | `.cursor/skills/matt-pocock/` (ask-matt·tdd·implement 등 30개), `.agents/` 없음 | **불일치.** override 표에 없다. 경로가 다르면 R8 사다리 3번이 비어 버린다 |
| 포니테일 | `unity-basics.mdc` L42: 프로젝트 `.cursor/skills/ponytail/` | `.cursor/skills/ponytail/` 있음 | 일치 |
| 티켓 경로 | R9: `docs/plan/tickets/` | `docs/project/plan/tickets/` | 허용 범위 (override 표 "문서 루트 `docs/project/`" L120~ 로 설명됨) |
| **위키 계약·결정 트리 중복** | R13: 규칙 본문은 Kit 문서에만 | `docs/project/README.md` §위키 운영 L8~ 이 Kit §에이전트 위키 계약과 거의 같다. §어디에 쓸지 (결정 트리) L127~ 이 Kit L47~ 과 거의 같고, L152 "**결정 트리 SSOT: 이 섹션.** Optimization·Kit은 링크로 위임" | **충돌.** 같은 결정 트리에 SSOT가 둘이다. Kit 트리에는 ADR 분기가 있지만 dragon 트리와의 문구 차이는 줄 단위로 대조하지 않았다(unknown) |
| 정본 사다리 | R7: 코드 ≥ Architecture ≥ 설계 정본. 외부 자료는 확인용(L196), Notion 덤프 금지(L19) | `docs/project/README.md` L82 사다리 2순위 "`architecture/` · Notion" | **충돌 후보 — 검증 필요.** Notion export는 `.gitignore` 대상(`docs/notion/`, L96)이라 repo에서 확인할 수 없다 |
| **Status 어휘** | R10: triage 5종만 | 티켓 `Status:` 실측: done 28 · resolved 16 · ready-for-agent 10 · ready-for-human 1 · in-progress 1 (`docs/project/plan/tickets/*/issues/*.md`, 주석 붙은 변형 포함) | **불일치.** 그러나 원인은 Kit 쪽이다. Kit에 완료·진행 상태가 없어서 dragon이 자체 어휘를 만들었다 |
| DoD | R11 (모호) | dragon 보고서 §8.4: DoD 없음 | 양쪽 다 없음. Kit 먼저 정해야 한다 |
| 문체 | R14: game 타이틀 `docs/`·`AGENTS.md`에도 한다체. 레거시는 손댄 구간만 | 합니다체·세요체 문장이 있는 문서 142/346 (`AGENTS.md`·`docs/project/README.md` 포함) | **불일치(레거시).** Kit도 "신규·수정 구간만" 요구하므로 일괄 수정 대상은 아니다 |
| GDD 태그 | R12: `locked`·`draft`·`vision`·`open`·`parked` | GDD 39개 중 Kit 태그를 쓰는 문서 0개, "Stub" 표기 21개 | **불일치** |
| README 허브·파일명 | R12: bare `UI.md`/`Combat.md` 금지 | `docs/project/` 아래 단어형 파일명 39개 (예: `gdd/03-systems/03-2-combat/Combat.md`, `AI.md`, `Items.md`, `Content.md` 2개) | **불일치.** 대부분 GDD 번호 폴더 안이라 문맥은 폴더가 준다. 개명 여부는 판단 보류 |
| Architecture 250줄 | R12 (검토 신호, 강제 아님) | 47개 중 8개 초과: CharacterAnimator 414 · Stage 352 · Stat 311 · Character 308 · Inventory 290 · Addressables 282 · GameApp 270 · Quest 261 | 검토 신호 |
| Assets 배치 | R15 | override 표 L125 `Assets/Scripts/`, L127 TSFramework 임베드, AddressableLayout 임베드 | **선언된 override → 절차상 일치.** dragon 2단계 V1(Resources 경로)은 코드가 걸린 문제라 **검증 필요** 그대로 둔다 |
| const 네이밍 | R16: PascalCase | override 표 L128 `UPPER_SNAKE_CASE` + 실측 근거 | **모범 사례** (Kit 방식대로 override 표에 근거와 함께 적음) |

### 3.3 Kit에 없는 규칙 (제안)

모두 제안이다. 현재 Kit에는 없다.

| 제안 | 넣을 곳 | 내용 | 해결하는 문제 |
|---|---|---|---|
| S1 완료 계열 Status 어휘 표 | `templates/docs/agents/triage-labels.md` + `DevelopmentProcess.md` §Issue tracker | triage 5종에 `in-progress`·`done`(·필요하면 `superseded`)을 더하고, Plan·Architecture·GDD 상태와의 대응표를 둔다. L131 "archive 또는 Completed"를 이 어휘로 바꾼다 | dragon C4 (Status 4종 이상 혼재), done/resolved 중복 |
| S2 DoD 정의 분리 | `DevelopmentProcess.md` §닫기 어휘 L128 | "DoD"를 *착수 조건*(Definition of Ready: acceptance·SC 합의 → `ready-for-agent`)과 *완료 조건*(Verify 통과 + 바뀐 페이지 Record + Status `done`)으로 나눈다 | L93과 L128의 뜻 충돌 |
| S3 템플릿에 DoD·Status 행 | `templates/AGENTS.game.md` §프로세스 · 문서 L43~ | S1·S2로 가는 한 줄 링크 + override 표에 "Status 어휘" 행 | 소비 repo마다 따로 만드는 문제 |
| S4 작업 유형별 읽기 규칙 | `docs/game/Documentation.md` §에이전트 위키 계약 아래 + 템플릿 | 버그 수정 / 리팩터 / 밸런스·데이터 / 신규 기능 설계 / 부트·로딩별로 "먼저 읽을 문서 종류" 표. 타이틀은 경로만 채운다 | dragon §1 "작업 유형별 라우팅 규칙 없음" |
| S5 테스트 실행 주체 | `UnityCliAgent.md` + `DevelopmentProcess.md` L22·L129 | "`/tdd`의 red/green 확인은 사용자가 래퍼나 Test Runner로 실행하고 결과를 넘긴다. 에이전트는 테스트 코드 작성과 컴파일 확인까지" 같은 문장 하나 | KC1, dragon C5 |
| S6 커밋 이슈 참조 정책 | `CommitMessages.md` §본문 · Footer L83 + §프로젝트에 둘 것 L151 | 이슈 참조를 footer로만 할지, 제목 접미사 `(#n)`을 프로젝트 override로 허용할지 정한다. 허용하면 override 표 항목에 추가 | dragon GIT_CONVENTIONS 이슈 번호 필수와의 충돌 |
| S7 `revert` type 정책 | `CommitMessages.md` §Type L28 | Conventional Commits의 `revert`를 쓸지 정한다 | dragon `AGENTS.md` L101 |
| S8 override 가능 항목 목록 | `AgentWorkflow.md` §정본 우선순위 | 프로젝트가 바꿀 수 있는 항목(경로·scope·언어·const·Issue tracker·Status 오른쪽 열 …)을 표로 고정 | "override 표에 없는 override"를 걸러낼 기준 |
| S9 Kit 자체 진입 문서 | 루트 `AGENTS.md` (신규 파일 제안 — 현재 없음) | Kit를 고칠 때의 규칙(docs 먼저 → mdc 요약, 한다체, 템플릿 변경 시 소비 repo 영향) | 프로필 규칙이 Kit 편집 때 섞이는 문제(`game/documentation.mdc` L12) |
| S10 Architecture 목적 이탤릭 기준 | `Documentation.md` L105·L114~144 | 골격의 이탤릭 문구가 "그대로 복사할 고정 문구"인지 "문서마다 다시 쓸 자리 표시"인지 밝힌다 | KC5, dragon 보고서 P2-2 판정 |

### 3.4 dragon 보고서에서 다시 봐야 할 판정 (dragon 보고서는 수정하지 않음)

- **C6 / P0-5 일부:** dragon `AGENTS.md` L14·L18의 `.cursor/rules/common/`·`.cursor/rules/game/`은 Kit 표 안의 경로이고, Kit에 실제로 있다(Kit tree `.cursor/rules/common/` 9개·`game/` 6개). 따라서 "없는 `.cursor/rules/*` 언급을 지운다"(dragon 보고서 P0-5)는 맞지 않을 수 있다. 문제는 존재 여부가 아니라 **두 번째 경로에 `unity-studio-kit/` 접두어가 없어 dragon repo 경로로 읽힐 수 있다**는 점이다. 이 표기는 Kit 템플릿 L11·L13에서 왔다. L200의 "`.cursor/skills/`가 있는데 없다고 적음" 지적은 그대로 유효하다.
- **§4.4 / P2-2 "템플릿 안내 이탤릭 43개 삭제":** Kit `Documentation.md` L105는 각 `##` 아래 목적 이탤릭 한 줄을 **요구**한다. dragon 43개 문서의 문구("*이 기능이 지금 무엇을 보장하는지 lead로 요약합니다…*")는 Kit 골격 L114의 옛 합니다체 문구와 같다. 지우면 Kit 규칙을 어기게 되므로, S10을 정한 뒤 "고정 문구를 문서별 목적 문장으로 바꾼다"로 바꾸는 것이 맞아 보인다.
- **C2 (이슈 번호 규칙):** dragon 내부 불일치였던 것이 Kit 기준으로는 "override 범위 밖 규칙"이기도 하다. 처리 방향은 S6 결정에 달려 있다.

## 4. Kit 내부 중복·충돌·깨진 링크·옛 라벨

### 4.1 중복 (K)

docs(사람 정본)와 `.mdc`(요약)의 이원화는 Kit가 의도한 구조이다(`WritingGuide.md` §docs와 rules). 아래는 그 밖의 중복이다.

| ID | 주제 | 위치 | 판단 |
|---|---|---|---|
| K1 | 커밋 규칙 | `CommitMessages.md` (정본) · `commit-messages.mdc` · `UnityBasics.md` §Git / 커밋 L28~38 · `unity-basics.mdc` §Git / Commit L25~30 · `templates/AGENTS.game.md` L50·§커밋 (이 repo) L81~ | 정본 1 + 요약 4. 모두 같은 내용이지만 `UnityBasics.md`와 `unity-basics.mdc`가 형식(`<type>(<scope>): <한글 제목>` + 본문 필수)까지 다시 적는다. 링크 한 줄로 줄이면 갱신 지점이 줄어든다 |
| K2 | 우선순위 사다리 | `AgentWorkflow.md` §정본 우선순위 · `agent-scope.mdc` §정본 우선순위 · `DevelopmentProcess.md` §스킬·규칙 우선순위 · `development-process.mdc` §우선순위 · `WritingGuide.md` §정본 사다리 · `Documentation.md` L196~199 · `documentation.mdc` L31 · `writing-guide.mdc` L19 | 내용은 서로 맞는다. 다만 7곳에 흩어져 있어, 하나를 바꾸면 나머지를 같이 바꿔야 한다 |
| K3 | Unity CLI 금지 | `UnityCliAgent.md` · `unity-cli-agent.mdc` · `unity-basics.mdc` L38 · `AgentWorkflow.md` §검증 · `agent-scope.mdc` L37 · `verification-qa-defaults.mdc` L24 · `unity-build-pipeline/SKILL.md` L35 | 내용은 일치한다. 2801ef8(2026-10-28 22:18 KST) 한 커밋으로 같이 들어갔다 |
| K4 | Architecture 골격 | `Documentation.md` §Architecture 작성 규약 · `documentation.mdc` §Architecture Must · `personal/documentation.mdc` §Architecture Must · `DocsLite.md` L37 · `WritingGuide.md` §Architecture | 요약은 링크로 정본을 가리킨다. 문제 없음 |

### 4.2 충돌 (KC)

| ID | 내용 | 근거 | 판정 |
|---|---|---|---|
| KC1 | Build 단계는 `/tdd` seam 테스트를 요구하지만, 에이전트는 Unity 테스트를 실행할 수 없다. 누가 red/green을 확인하는지 정해지지 않았다 | `DevelopmentProcess.md` L20·L22·L129 ↔ `UnityCliAgent.md` L13 · `unity-cli-agent.mdc` L12~13 | 충돌 (dragon C5의 원인 중 하나) |
| KC2 | DoD의 닫힘이 `Status: ready-for-agent`(착수 가능)이고, 작업 완료는 §닫기 L93이 따로 정의한다. Record의 "archive 또는 Completed"는 Status 어휘에 없다 | `DevelopmentProcess.md` L93 · L128 · L131 ↔ `triage-labels.md` | 충돌 (어휘 미정의) |
| KC3 | behavioral Verify는 Plan「확인」을 쓰는데, QA 규칙은 Plan에 수동 시나리오 섹션을 요청 없이 넣지 말라고 한다. 「확인」이 그 섹션에 해당하는지 경계가 없다 | `DevelopmentProcess.md` L91·L100 ↔ `verification-qa-defaults.mdc` L20 | 경미한 충돌 (해석 필요) |
| KC4 | Kit 참조는 텍스트 경로로 하라고 평가표가 요구하지만, 템플릿은 `unity-studio-kit/...`를 markdown 링크로 쓴다. 복사된 repo 안에서는 깨진다 | `RulesEvaluationScorecard.md` L144 (7.4) ↔ `templates/AGENTS.game.md` L78 · `templates/AGENTS.personal.md` L46 | 충돌. dragon `AGENTS.md` L136에 실제로 복제됨 |
| KC5 | 목적 이탤릭은 "각 `##` 아래 한 줄로 적는다"인데, 골격에 고정 문구가 들어 있다. 복사해 두면 되는지, 다시 써야 하는지 알 수 없다. 골격 L136은 아직 합니다체("모읍니다")이다 | `Documentation.md` L105 ↔ L114~144 | 모호 |
| KC6 | Kit는 타이틀 특수 규칙을 넣지 않는다고 하면서, personal 규칙에 Dragon 타입 이름을 적는다 (금지 문장 안의 예시) | `game-profile.mdc` L26 · `docs/personal/Overview.md` L40 ↔ `personal/demo-gui.mdc` L30 · `docs/personal/DemoGui.md` L69 | 경미 (예시로 남길지 판단 필요) |
| KC7 | Kit가 스스로 정한 한다체 규칙을 Kit 본문이 어긴다. 해요체·합니다체 11줄, 한다체 기계 변환 오탈자 21줄("두한다"·"맞추한다"·"고치한다"·"여한다"·"되돌리한다"·"넘기한다"·"평간다"·"흔한다"·"붙이다."·"얹다." 등) | 해요체: `AgentWorkflow.md` L14 · `ProjectSeparation.md` L28 · `LocaleDocs.md` L7. 합니다체: `Documentation.md` L5·L77·L85·L88·L98·L136·L174 · `unity-build-pipeline/SKILL.md` L14. 오탈자: §1.1 표 각 행 · `CommitMessages.md` L22·L153 · `WritingGuide.md` L32·L41·L53·L60 · `templates/AGENTS.*.md` L7 · `triage-labels.md` L13 · `issue-tracker.md` L13 · `agent-scope-game.mdc` L8 · `PackageLayout.md` L21 등 | 충돌 (자기 규칙 위반). 오탈자 대부분이 f5a08f1 "Kit 문서·규칙 문체를 한다체로 통일"(2026-10-18 12:08 KST) 이후 파일에 있다. 그 커밋에서 생겼는지는 diff를 보지 않아 unknown |

### 4.3 깨진 링크·옛 라벨

깨진 상대 링크 (md·mdc 전체, 코드 블록 제외, 기계 검사):

| 위치 | 링크 | 문제 |
|---|---|---|
| `.cursor/rules/personal/documentation.mdc` L33 | `../game/Documentation.md#readme-허브` | `.cursor/rules/game/Documentation.md`로 풀려 없는 파일이다. 의도한 대상은 `../../../docs/game/Documentation.md#readme-허브`로 보인다 |
| `templates/AGENTS.game.md` L78 | `unity-studio-kit/docs/common/UnityCliAgent.md` | Kit 안에서도, 복사된 타이틀 repo 안에서도 풀리지 않는다 (KC4) |
| `templates/AGENTS.personal.md` L46 | 위와 같음 | 위와 같음 |
| `.cursor/rules/common/agent-scope.mdc` L20 · `docs/common/AgentWorkflow.md` L22 | `DevelopmentProcess.md#스킬·규칙-우선순위` | **깨졌을 가능성이 높음 — 검증 필요.** GitHub 앵커 생성은 문장부호를 지우므로 `·`가 빠진 `#스킬규칙-우선순위`가 될 것으로 본다. 브라우저로 확인하지는 않았다 |

디렉터리 링크(`docs/common/README.md` L20의 `.cursor/rules/common/` 등)는 대상 폴더가 있어 정상으로 쳤다. 다른 앵커(`#에이전트-위키-계약`·`#어디에-쓸지-결정-트리`·`#architecture-작성-규약`·`#결정-기록-라우팅`·`#optimization-운영`)는 헤딩과 맞는다.

옛 라벨:

| 위치 | 문구 | 현재 상태 (근거) |
|---|---|---|
| `README.md` L61 | "common 중 기본·스코프·**포니테일**·Shell·Unity CLI는 alwaysApply" | 포니테일 규칙은 0788460(2026-10-25 14:55 KST)에서 Kit에서 빠지고 프로젝트 스킬로 바뀌었다. 지금 alwaysApply는 4개 (§1.2) |
| `README.md` L57 | `skills/ ← Cursor Agent skill (**리뷰·Design**·DOTS·빌드)` | 리뷰·Design 스킬은 ea68000(2026-10-18 20:39 KST)에서 타이틀 `.agents/skills/`로 옮겨졌다. Kit에는 DOTS·빌드 2개뿐 |
| `game/game-profile.mdc` L13 · `personal/personal-profile.mdc` L13 | "common(**포니테일**·스코프·.meta·Shell·C#)은 그대로 적용" | 위와 같음. common에는 포니테일 규칙이 없다 |
| `templates/AGENTS.game.md` L54 | "Kit common C#·네이밍·**포니테일**" | 위와 같음 |
| `README.md` L88 | "리뷰·Design·아키텍처 스킬 — mattpocock/skills (MIT)" | 출처 고지라 남겨도 되지만 Kit에 그 스킬이 없다는 점을 밝히면 덜 헷갈린다 (판단 보류) |

## 5. 정리 계획

모두 제안이다. 저장소는 바꾸지 않았다. 공수는 사람이 손으로 고칠 때의 대략값이다.

### P0 — 소비 repo에 잘못된 규칙이 퍼지거나 에이전트가 바로 헷갈리는 것

| ID | 파일 | 방법 | 이유 | 공수 |
|---|---|---|---|---|
| P0-1 | `templates/docs/agents/triage-labels.md` · `docs/game/DevelopmentProcess.md` §닫기 어휘 L128·L131 | 완료 계열 Status(`in-progress`·`done` 등)를 더한 어휘 표를 만들고, DoD를 착수 조건/완료 조건으로 나눈다 (S1·S2) | KC2. dragon Status 혼재(done 28·resolved 16)의 원인 | 1시간 |
| P0-2 | `docs/common/UnityCliAgent.md` · `DevelopmentProcess.md` L22·L129 | `/tdd`·seam 테스트를 누가 실행하는지 한 문장으로 정한다 (S5) | KC1. dragon C5 | 30분 |
| P0-3 | `docs/common/CommitMessages.md` §본문 · Footer · §프로젝트에 둘 것 · §Type | 이슈 번호를 제목에 넣을 수 있는지(override 허용 여부)와 `revert` 허용 여부를 정한다 (S6·S7) | dragon 커밋 규칙이 Kit override 범위 밖. 정해지지 않으면 dragon 쪽을 고칠 기준이 없다 | 30분 |
| P0-4 | `templates/AGENTS.game.md` · `AGENTS.personal.md` | L78/L46 링크를 텍스트 경로로 바꾸고, L11·L13 두 번째 경로에 `unity-studio-kit/` 접두어를 붙이고, L54 포니테일을 고치고, DoD·Status 한 줄과 override 표 "Status 어휘" 행을 더한다 (S3) | KC4. 복사할 때마다 결함이 퍼진다 | 1시간 |
| P0-5 | `README.md` L57·L61 · `game/game-profile.mdc` L13 · `personal/personal-profile.mdc` L13 · `personal/documentation.mdc` L33 | 옛 라벨 4곳과 깨진 링크 1곳을 고친다 | 진입 문서와 프로필 규칙이 없는 규칙을 가리킨다 | 20분 |

### P1

| ID | 파일 | 방법 | 이유 | 공수 |
|---|---|---|---|---|
| P1-1 | `docs/game/Documentation.md` §에이전트 위키 계약 · 템플릿 | 작업 유형별 읽기 규칙 표를 더한다 (S4) | 작업 유형별 라우팅이 Kit·dragon 양쪽에 없음 | 1~2시간 |
| P1-2 | `docs/common/AgentWorkflow.md` §정본 우선순위 | override 가능한 항목 목록을 고정한다 (S8) | "표에 없는 override"를 판별할 기준 | 1시간 |
| P1-3 | 프로필 `.mdc` 7개 (globs 없음) | 실제 로드 여부를 관찰한다(`RulesEvaluationScorecard.md` §1·§2). 안 붙으면 `alwaysApply`나 globs를 검토한다 | §1.2 검증 필요 | 1시간 (관찰) |
| P1-4 | `docs/game/Documentation.md` L105·L114~144 | 목적 이탤릭이 고정 문구인지 자리 표시인지 밝히고 L136 문체를 고친다 (S10) | KC5. dragon P2-2 판정이 이것에 달려 있다 | 30분 |
| P1-5 | `DevelopmentProcess.md` §Verify · `verification-qa-defaults.mdc` L20 | Plan「확인」과 "수동 시나리오 섹션"의 경계를 한 줄로 정한다 | KC3 | 20분 |

### P2

| ID | 파일 | 방법 | 이유 | 공수 |
|---|---|---|---|---|
| P2-1 | §4.2 KC7 목록의 파일들 | 해요체·합니다체 11줄과 변환 오탈자 21줄을 고친다 | 자기 규칙 위반 | 1시간 |
| P2-2 | `docs/common/UnityBasics.md` §Git / 커밋 · `unity-basics.mdc` §Git / Commit | 커밋 형식 반복을 링크 한 줄로 줄인다 | K1 | 15분 |
| P2-3 | `docs/game/README.md` | `적용` 열을 더해 common·personal 허브와 형식을 맞춘다 | 작업 시점별 읽기 안내 | 15분 |
| P2-4 | `.cursor/skills/unity-ecs-patterns/references/details.md` (585줄) | 주제별 분리를 검토한다 | 500줄 초과 | 1시간 |
| P2-5 | 루트 `AGENTS.md` (현재 없음, 새 파일 제안) | Kit 편집용 진입 문서 (S9) | Kit 자체 작업 규칙의 진입점이 없다 | 30분 |
| P2-6 | `personal/demo-gui.mdc` L30 · `DemoGui.md` L69 | Dragon 타입 이름을 일반 표현으로 바꿀지 정한다 | KC6 | 10분 |

### 5.4 권장 순서: Kit 먼저, 그다음 dragon

1. **Kit P0-1~P0-3** (규칙 결정). 이 결정이 dragon 정리의 기준이다.
2. **Kit P0-4·P0-5** (템플릿·진입 문서). 이후 새 repo로 결함이 퍼지지 않는다.
3. **Kit P1-4** (이탤릭 기준). dragon P2-2를 처리하기 전에 필요하다.
4. **dragon 정리** — dragon 보고서 §7과 함께:
   - 커밋: P0-3 결정에 맞춰 `GIT_CONVENTIONS.md` §이슈 번호 규칙을 AGENTS 커밋 표로 옮기거나 지운다. 정본을 Kit + AGENTS 하나로 접는다 (dragon C1·C2).
   - Issue tracker·스킬 경로: `AGENTS.md` §이 타이틀 override 표에 "Issue tracker (로컬+GitHub 쌍)"와 "스킬 경로 `.cursor/skills/matt-pocock/`" 행을 더한다. 아니면 Kit 경로에 맞춘다.
   - Status: P0-1 어휘로 티켓 `Status:`를 맞춘다 (dragon C4).
   - 테스트: P0-2 문장에 맞춰 `matt-pocock/implement/SKILL.md` L27을 고친다 (dragon C5).
   - 위키 계약·결정 트리: `docs/project/README.md` §위키 운영·§어디에 쓸지의 본문을 Kit 링크 + 타이틀 경로로 줄이고 L152 SSOT 선언을 정리한다.
   - Kit 링크: `AGENTS.md` L136 링크를 텍스트 경로로 바꾼다. L14·L18 접두어를 붙인다. 이때 dragon 보고서 P0-5의 "없는 `.cursor/rules/*` 언급 삭제"는 §3.4를 보고 다시 판단한다.
5. **Kit P1·P2, dragon P1·P2** 나머지.

## 6. 읽은 범위와 못 본 것

읽은 것
- Kit main `c843416` 트리 전체와 텍스트 파일 56개 전문: md 33 · mdc 20 · `NOTICE` · `LICENSE` · `.gitignore`. README·docs/common·docs/game·docs/personal·templates·rules 전 파일은 본문까지 읽었다. 스킬은 `SKILL.md` 2개와 `ci-build-script.md`는 읽었고, `unity-ecs-patterns/references/details.md`(585줄)는 기계 검사(링크·문체·키워드)만 했다.
- 커밋 29개의 메시지와 파일별 마지막 변경 커밋.
- dragon 대조: `/workspace/mirror`(dragon main `340e742`)의 `AGENTS.md`·`GIT_CONVENTIONS.md`·`docs/project/README.md`·`.cursor/skills/` 목록·`matt-pocock/implement/SKILL.md` L27, 티켓 `Status:` 줄, 문서 전체에 대한 문체·파일명·줄 수 기계 검사.

못 본 것 / 확인 못 한 것
- Cursor가 멀티 루트의 두 번째 루트(Kit) `.cursor/rules`를 실제로 로드하는지, globs 없는 `alwaysApply: false` 규칙이 언제 붙는지 (동작 관찰 불가 → 검증 필요).
- GitHub 앵커 `#스킬·규칙-우선순위`가 실제로 깨지는지 (브라우저로 확인하지 않음).
- 한다체 오탈자가 f5a08f1에서 생겼는지 (커밋 diff를 보지 않음).
- dragon `docs/notion/`(gitignore) 내용 — 그래서 Notion을 정본 사다리에 둔 것이 Kit L196과 충돌하는지는 검증 필요.
- dragon 결정 트리와 Kit 결정 트리의 줄 단위 차이, dragon 코드가 Kit AssetsLayout을 따르는지 (코드는 읽지 않음).
- Kit의 브랜치·PR·이슈 (main만 봄).
