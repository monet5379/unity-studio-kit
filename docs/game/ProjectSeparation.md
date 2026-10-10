# 공통 / 게임 분리 (game)

공유 Core UPM·타이틀 Game·에디터 전용 코드를 **어셈블리(asmdef) 경계**로 나눠, 재사용·빌드·컴파일 책임이 섞이지 않게 해요. 무엇을 Core에 두고 Game·Editor에 둘지는 이 페이지에서 정하고, 폴더 배치는 [AssetsLayout.md](AssetsLayout.md)를 봐요.

Cursor: [`agent-scope-game.mdc`](../../.cursor/rules/game/agent-scope-game.mdc)

## 왜 나누나요

Unity `Editor/` 폴더만으로도 **플레이어 빌드에서 에디터 스크립트를 빼는 것**은 대부분 됩니다. game 프로필에서는 이미 **Core·Game asmdef**로 모듈을 쓰므로, **Editor 전용 asmdef**까지 두어 참조 방향과 **증분 컴파일 단위**를 맞추는 것을 표준으로 해요.

### Shared Core (Runtime)

Core가 타이틀 enum·세이브·스테이브를 **이름으로 참조**하기 시작하면, 다음 타이틀·패키지 재사용이 막혀요. 장르 무관 인프라(리소스 로드 골격, Json 파이프, 공통 유틸 등)만 Core에 두고, 타이틀 도메인 타입은 Game 쪽에 둬요.

Core asmdef는 **Game asmdef를 references에 넣지 않아요.** Game → Core 한 방향만 허용해요.

### Game (Runtime)

타이틀 로직·콘텐츠·도메인은 Game asmdef에 모아요. Core를 참조하고, 공유 패키지 **소스**는 소비 타이틀 repo에서 직접 고치지 않아요(manifest pin · 호출 코드만).

Game을 Core와 나누면 **“다음 프로젝트에 가져갈 코드”**와 **“이 게임만의 코드”**가 컴파일·리뷰 단위로도 갈라져요.

### Editor (에디터 전용 asmdef)

`Project/Editor/`(또는 Core UPM 안 `Editor/`)에 **Editor asmdef**(`includePlatforms: Editor`)를 두어요.

- **빌드·API 경계:** Runtime asmdef(Core·Game)는 `UnityEditor`·에디터 전용 패키지를 references에 두지 않아요. 에디터 툴·CustomEditor·빌드/검증 메뉴는 Editor asmdef에만 둬요.
- **컴파일 단위:** 부모 asmdef 아래 `Editor/` 폴더만 쓰면 스크립트는 빌드에서 빠질 수 있지만, **같은 asmdef에 Runtime과 묶인 채** 재컴파일되는 경우가 많아요. Editor asmdef를 쪼개면 툴 수정과 게임 Runtime 수정의 영향 범위를 나눌 수 있어요.
- **참조 방향:** Editor asmdef → Core·Game(Runtime) 참조는 흔해요. **Runtime → Editor asmdef 참조는 금지**예요.

에디터에서 씬·프리팹을 Setup 스크립트로 생성·배선하지 않는 규칙은 [UnityBasics](../common/UnityBasics.md)예요. Editor asmdef는 그 **역할(검증·빌드·임포트·툴링)** 과 맞춰요.

(선택) 장르 공통 전투 층을 Game과 Core 사이에 두면, Core ← 중간층 ← Game 참조만 써도 돼요.

## 층

| 층 | asmdef | 역할 | 규칙 |
|----|--------|------|------|
| **Shared Core** | Core (Runtime) · (선택) Core.Editor | 장르 무관 재사용 | 타이틀 enum·세이브·스테이지 **이름 참조 금지**. Game asmdef 참조 금지 |
| **Game** | Game (Runtime) | 타이틀 로직·도메인 | Core 참조. 공유 패키지 소스 직접 수정 금지 |
| **Editor** | Game.Editor · (선택) Core.Editor | Inspector·메뉴·빌드/검증·임포트 | Runtime asmdef 참조 가능. Runtime이 Editor asmdef 참조 금지 |
| **ThirdParty / Develop** | Game 쪽 (Runtime) | SDK 어댑터 · 디버그 | 벤더 원본 수정 금지 · `ThirdPartyAdapters` 등 Game에 래퍼 |

타이틀별 asmdef **이름·경로**(예: 임베드 프레임워크) override는 **그 게임 repo** `AGENTS.md`에 적어요.

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
