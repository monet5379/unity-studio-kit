# 규칙 평가 스코어카드

Kit의 `.cursor/rules` · `docs/` · `templates/` · `.cursor/skills`를 한 바퀴 돌며 **일관성·적용 가능성·정본 사다리**를 점검할 때 쓴다. 블록마다 정본 링크를 열고, 아래 등급과 메모 칸을 채운 뒤 §횡단 패스에서 충돌만 모아서 정리한다.

**대상:** unity-studio-kit 저장소 자체, 또는 **프로젝트 + Kit 멀티 루트**에서 Kit 규칙이 실제로 어떻게 켜지는지 확인할 때.  
**프로필:** personal / game은 **각각 한 트랙**으로 평간다 (동시 필수 아님).  
**타이틀:** 프로젝트 `AGENTS.md` · `.cursor/rules/<title>/`는 §7 레이어로 같은 체크리스트를 적용한다.

관련: [AgentWorkflow.md](AgentWorkflow.md) · [WritingGuide.md](WritingGuide.md) · [루트 README](../../README.md)

## 등급 (블록 공통)

| 등급 | 의미 | 판단 질문 |
|------|------|-----------|
| **A** | 그대로 유지 | 에이전트가 매 턴 지킬 수 있고, docs만 읽어도 사람과 결론이 같음 |
| **B** | 소폭 정리 | 요약·링크·glob·한두 문장만 고치면 됨 |
| **C** | 구조 이슈 | mdc↔docs 불일치, personal/game 동시 필수, 우선순위 모호 |
| **D** | 위험·누락 | Must not 위반 유도, 안전 레일(`.meta`·Shell) 구멍, dead link |
| **—** | 해당 없음 | 이번 평가 범위 밖 (선택 문서·미사용 프로필) |

블록별 **세부 질문 (예/아니오)** — 하나라도 «아니오»면 등급을 한 단계 내립니다.

1. Must / Must not이 판단 가능한가 (모호한 «적절히»만 있지 않은가)
2. `.mdc`가 docs 전문을 복제하지 않고, 링크가 살아 있는가
3. `alwaysApply` · glob · `profile:` 전제가 README와 같은가
4. 다른 블록과 **우선순위**가 문서에 적혀 있는가 (없으면 §6에서 기록)

## 0. 평가 프레임 (세션 시작)

| 항목 | 메모 |
|------|------|
| 평가 일자 · 평가자 | |
| 범위 (Kit만 / Kit+프로젝트명) | |
| 막고 싶은 실패 (예: `.meta` 수정, 과잉 Plan) | |
| 사용 프로필 (`personal` / `game` / 둘 다 트랙) | |
| 배선 확인 (새 채팅에서 소비 프로젝트 파일을 Read한 뒤 첨부된 규칙을 관찰. frontmatter 추론으로 대신하지 않음) | |

---

## 1. 배선 · 진입

| ID | 정본 · 규칙 | 등급 | 메모 |
|----|-------------|------|------|
| 1.1 | [README.md](../../README.md) — 3층·멀티 루트·skill 위치 | | |
| 1.2 | [docs/common/README.md](README.md) — common 목록 | | |
| 1.3 | [templates/README.md](../../templates/README.md) · `AGENTS.*.md` — override · 복사 후 Kit 참조 유효 | | |

---

## 2. Common · alwaysApply

| ID | `.mdc` | `docs/` 정본 | 등급 | 메모 |
|----|--------|--------------|------|------|
| 2.1 | [agent-scope.mdc](../../.cursor/rules/common/agent-scope.mdc) | [AgentWorkflow.md](AgentWorkflow.md) §스코프 | | |
| 2.2 | (프로젝트) `.cursor/skills/ponytail/` | AgentWorkflow §포니테일·§검증 | | |
| 2.3 | [unity-basics.mdc](../../.cursor/rules/common/unity-basics.mdc) | [UnityBasics.md](UnityBasics.md) | | |
| 2.4 | [shell-destructive-ops.mdc](../../.cursor/rules/common/shell-destructive-ops.mdc) | [ShellSafety.md](ShellSafety.md) | | |
| 2.5 | [unity-cli-agent.mdc](../../.cursor/rules/common/unity-cli-agent.mdc) | [UnityCliAgent.md](UnityCliAgent.md) | | |

---

## 3. Common · glob · 주제별

| ID | `.mdc` | `docs/` 정본 | 트리거 | 등급 | 메모 |
|----|--------|--------------|--------|------|------|
| 3.1 | [commit-messages.mdc](../../.cursor/rules/common/commit-messages.mdc) | [CommitMessages.md](CommitMessages.md) | 커밋 요청 시 (description · unity-basics 요약) | | |
| 3.2 | [csharp-standards.mdc](../../.cursor/rules/common/csharp-standards.mdc) | [Csharp.md](Csharp.md) | `**/*.cs` | | |
| 3.3 | [naming-semantics.mdc](../../.cursor/rules/common/naming-semantics.mdc) | Csharp (보완) | `**/*.cs` | | |
| 3.4 | [writing-guide.mdc](../../.cursor/rules/common/writing-guide.mdc) | [WritingGuide.md](WritingGuide.md) | docs·AGENTS | | |
| 3.5 | [dev-imgui.mdc](../../.cursor/rules/common/dev-imgui.mdc) | [DevImgui.md](DevImgui.md) | IMGUI glob · **선택** | | |

---

## 4A. Personal 트랙 (`profile: personal`)

| ID | `.mdc` / 문서 | 등급 | 메모 |
|----|---------------|------|------|
| 4A.1 | [personal-profile.mdc](../../.cursor/rules/personal/personal-profile.mdc) · [Overview.md](../personal/Overview.md) | | |
| 4A.2 | [package-layout.mdc](../../.cursor/rules/personal/package-layout.mdc) · [PackageLayout.md](../personal/PackageLayout.md) | | |
| 4A.3 | [DocsLite.md](../personal/DocsLite.md) · [documentation.mdc](../../.cursor/rules/personal/documentation.mdc) | | |
| 4A.4 | [locale-docs.mdc](../../.cursor/rules/personal/locale-docs.mdc) · [LocaleDocs.md](../personal/LocaleDocs.md) | | |
| 4A.5 | [demo-gui.mdc](../../.cursor/rules/personal/demo-gui.mdc) · [DemoGui.md](../personal/DemoGui.md) · **선택** | | |
| 4A.∑ | game Plan·Verify·DevelopmentProcess가 personal에 **끌려 오지 않음** (Architecture 골격은 공유) | | |

---

## 4B. Game 트랙 (`profile: game`)

| ID | `.mdc` / 문서 | 등급 | 메모 |
|----|---------------|------|------|
| 4B.1 | [game-profile.mdc](../../.cursor/rules/game/game-profile.mdc) · [Overview.md](../game/Overview.md) | | |
| 4B.2 | [development-process.mdc](../../.cursor/rules/game/development-process.mdc) · [DevelopmentProcess.md](../game/DevelopmentProcess.md) | | |
| 4B.3 | [verification-qa-defaults.mdc](../../.cursor/rules/game/verification-qa-defaults.mdc) | | |
| 4B.4 | [unity-assets-layout.mdc](../../.cursor/rules/game/unity-assets-layout.mdc) · [AssetsLayout.md](../game/AssetsLayout.md) | | |
| 4B.5 | [agent-scope-game.mdc](../../.cursor/rules/game/agent-scope-game.mdc) · [ProjectSeparation.md](../game/ProjectSeparation.md) | | |
| 4B.6 | [documentation.mdc](../../.cursor/rules/game/documentation.mdc) · [Documentation.md](../game/Documentation.md) | | |
| 4B.7 | [templates/docs/agents/](../../templates/docs/agents/) · [plan/tickets/README.md](../../templates/docs/plan/tickets/README.md) | | |
| 4B.∑ | 타이틀 전용 규칙이 Kit game에 **새어 들지 않음** | | |

---

## 5. Skills (요청 · 단계 전용)

| ID | skill | 등급 | 메모 |
|----|-------|------|------|
| 5.1 | 타이틀 `.agents/skills/code-review` — Standards / Spec (Kit 중복 없음) | | |
| 5.2 | 타이틀 `.agents/skills/codebase-design` | | |
| 5.3 | 타이틀 `.agents/skills/improve-codebase-architecture` — **호출 전용** | | |
| 5.4 | [unity-ecs-patterns](../../.cursor/skills/unity-ecs-patterns/SKILL.md) | | |
| 5.5 | [unity-build-pipeline](../../.cursor/skills/unity-build-pipeline/SKILL.md) | | |
| 5.∑ | DevelopmentProcess · game-profile · code-review의 Verify/Design/리뷰 **용어 일치** | | |

---

## 6. 횡단 패스 (마지막)

| ID | 점검 | 등급 | 발견 · 조치 |
|----|------|------|-------------|
| 6.1 | 우선순위: 코드 ≥ Architecture ≥ 설계 정본 · `AGENTS` override | | |
| 6.2 | personal ↔ game 동시 필수 서술 없음 | | |
| 6.3 | glob 겹침 (`Assets/**`, C# naming, IMGUI) | | |
| 6.4 | README «안 하는 일» ↔ 실제 규칙 집합 | | |
| 6.5 | 선택 문서가 본편을 덮어쓰지 않음 | | |

### 시나리오 trace (선택)

| 시나리오 | 켜지는 규칙 (예상) | 실제와 일치? | 메모 |
|----------|-------------------|--------------|------|
| personal — README 계약만 수정 | | ☐ | |
| personal — Architecture + 코드 | | ☐ | |
| game — Architecture 한 장 + 티켓 | | ☐ | |
| Shell로 `Assets/` 정리 시도 | | ☐ | |
| «EditMode 테스트 실행해줘» | unity-cli-agent · 래퍼 안내만 | | ☐ | |

---

## 7. 타이틀 · 프로젝트 레이어 (Kit+프로젝트 평가 시)

| ID | 대상 | 등급 | 메모 |
|----|------|------|------|
| 7.1 | 프로젝트 `AGENTS.md` (`profile:` · scope · override) | | |
| 7.2 | `.cursor/rules/<title>/` (있다면) | | |
| 7.3 | Kit common + profile + 타이틀 **충돌 없음** | | |
| 7.4 | Kit 참조가 clone 위치와 무관 (텍스트 경로 `unity-studio-kit/...` · 드라이브 루트를 거치는 상대 링크 금지) | | |
| 7.5 | Kit와 다른 값이 모두 override 표에 있음 (예: C# const, 커밋 scope) | | |

---

## 요약

| 구역 | A | B | C | D | — |
|------|---|---|---|---|---|
| §1 배선 | | | | | |
| §2 alwaysApply | | | | | |
| §3 common glob | | | | | |
| §4A personal | | | | | |
| §4B game | | | | | |
| §5 skills | | | | | |
| §6 횡단 | | | | | |
| §7 타이틀 | | | | | |

**다음 액션 (최대 5개, why 위주):**

1.
2.
3.

**전체 판정:** ☐ 유지 ☐ 소폭 패치 ☐ 구조 정리 필요 ☐ 안전·정본 우선 수정
