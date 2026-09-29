# Assets 레이아웃 (game)

타이틀에서 파일이 어디로 가야 하는지 **폴더 결정**을 할 때 보세요. 공유 Core vs Game 코드 경계는 [ProjectSeparation.md](ProjectSeparation.md)예요.

Cursor: [`unity-assets-layout.mdc`](../../.cursor/rules/game/unity-assets-layout.mdc)  
설계 `.md`는 Unity 밖 `docs/`(또는 `Docs/`). Assets 안 README는 **20줄 이내**만.

## 최상위

```text
Assets/
├── Project/                 ← 팀 소유 (코드·씬·콘텐츠·에디터)
├── Addressables/            ← 런타임 로드 (JSON·SO …) — 복수형만; Addressable/ 금지
├── AddressableAssetsData/   ← Addressables 설정 (수동 GUID 편집 금지)
├── Resources/               ← 브리지·과도기 (신규 대량 콘텐츠 X → Addressables)
├── ThirdParty/              ← 벤더 SDK (직접 수정 금지)
├── Plugins/                 ← 네이티브·플랫폼 플러그인
├── Settings/                ← URP·Input 등
└── TextMesh Pro/
```

## Project/

```text
Project/
├── Scripts/                 ← Game asmdef · 도메인 폴더 (1기능 = 1최상위)
│   ├── <Domain>/
│   ├── ThirdPartyAdapters/  ← SDK 래퍼만
│   └── Develop/             ← 디버그 UI 등 (선택)
├── Editor/                  ← 게임 전용 Editor asmdef
├── Content/                 ← 아트·연출 (스크립트 X)
├── Scenes/
└── Tests/                   ← 선택
```

- **공유 Core**는 UPM `Packages/<shared-core>/` — `Assets/Project/Core/`에 임베드하지 않는 것을 표준으로 해요.
- Game이 Core를 참조해요. Core는 Game을 참조하지 않아요.
- 장르 공통 전투 층이 있으면 Game이 그 층을 참조하고, 그 층이 Core를 참조해요.
- `ThirdPartyAdapters`와 `Develop`는 Game 쪽에 둬요.

## 런타임 데이터 (3층)

| 층 | 형태 | 경로 |
|----|------|------|
| ① | enum 1:1 SO | `Addressables/Scriptable/<Category>/` |
| ② | Config SO | `Addressables/Scriptable/Config/` |
| ③ | Json 표·스트링 | `Addressables/JSON/` |

`Resources/`와 Addressables에 **동일 파일명 이중 등록 금지**예요.

## 금지

- `.meta` 생성·수정·삭제 (Shell 포함)
- Editor에서 씬·프리팹을 생성·수정·배선하는 Setup 스크립트 ([UnityBasics](../common/UnityBasics.md) 씬·프리팹 정본)
- ThirdParty·Plugins 직접 수정 (어댑터만 `Project/Scripts/ThirdPartyAdapters/`)
- 레거시 `Assets/Scripts/`에 신규 기능 추가 (표준은 `Project/Scripts/`)

타이틀별 실제 경로 override는 **그 게임 repo** `AGENTS.md` / AssetsLayout 오버레이에 적어요.
