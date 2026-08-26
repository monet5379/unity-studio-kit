# 공통 / 게임 분리 (game)

공유 패키지에 타이틀 전용 타입이 새지 않게, **무엇을 Core에 두고 무엇을 Game에 둘지**를 정해요.

**왜 나누나요?** Core가 타이틀 enum·세이브를 이름으로 참조하면, 다음 타이틀·패키지 재사용이 막혀요. 게임 로직은 Game에, 장르 무관 인프라는 Core에 둬요.

Cursor: [`agent-scope-game.mdc`](../../.cursor/rules/game/agent-scope-game.mdc)

## 층

| 층 | 역할 | 규칙 |
|----|------|------|
| **Shared Core** | 장르 무관 재사용 (리소스·씬 골격·Json 인프라 등) | 타이틀 enum·세이브·스테이지를 **이름으로 참조하지 않음**. Game asmdef 참조 금지 |
| **Game** | 타이틀 로직·콘텐츠·도메인 | Core를 참조. 공유 패키지 소스는 이 repo에서 직접 수정하지 않음 |
| **ThirdParty / Develop** | SDK 어댑터 · 디버그 | 벤더 원본 수정 금지 · Game 쪽에 래퍼 |

(선택) 장르 공통 전투 층을 빼면 Core ← Game만 써도 돼요.

## 문서 트리 (타이틀 repo)

| 트리 | 대상 |
|------|------|
| `docs/studio/` 또는 Kit + 공유 문서 | 공통 프로세스·프레임워크 Architecture (구현된 것만) |
| `docs/project/` 또는 `docs/<title>/` | 게임 도메인 Architecture · Plan · GDD |
| `docs/reference/` (선택) | 이전 타이틀 스냅샷 — 읽기 전용 |

**Architecture = 지금 있는 코드**예요. 목표·Phase는 Plan에 둬요.

## 에이전트

- 소비 타이틀에서는 공유 패키지 **소스·PackageCache**를 고치지 않아요 → manifest pin · 호출 코드만.
- 패키지 구현 변경은 **그 패키지 정본 repo**에서 해요.
- 물리 경로는 [AssetsLayout.md](AssetsLayout.md)예요.
