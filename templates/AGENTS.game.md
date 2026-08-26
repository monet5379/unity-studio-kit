# <GameTitle> — Agent Guide

```text
profile: game
```

출시·팀 타이틀용이에요. Cursor는 **이 repo + unity-studio-kit** 멀티 루트로 여세요.

| Kit | 경로 |
|-----|------|
| 공통 | `unity-studio-kit/docs/common/` · `.cursor/rules/common/` |
| 글쓰기 | `unity-studio-kit/docs/common/WritingGuide.md` |
| 프로필 | `unity-studio-kit/docs/game/` · `.cursor/rules/game/` |

타이틀 전용 규칙·경로는 **이 파일**과 (있으면) `.cursor/rules/<title>/`에만 둬요. Kit를 수정하지 마세요.

## 프로젝트 개요

- **장르·한 줄:** <…>
- **Git 루트:** 이 저장소 최상단
- **Unity 프로젝트:** `<UnityProjectFolder>/` (에셋·씬·스크립트는 여기만)

## 저장소 레이아웃

| 경로 | 용도 |
|------|------|
| `AGENTS.md` | 이 파일 |
| `docs/` 또는 `Docs/` | GDD · Architecture · Plan (타이틀 정본) |
| `<UnityProjectFolder>/Assets/` | 에셋 |
| `.cursor/rules/<title>/` | 타이틀 전용 Cursor 규칙 (선택) |

Kit Assets·문서 관례: `unity-studio-kit/docs/game/AssetsLayout.md` · `Documentation.md` · `DevelopmentProcess.md`

## 에이전트가 지킬 것

### Unity / 에셋

- `.meta` 생성·수정·삭제 금지.
- 공유 Core UPM **소스·PackageCache** 직접 수정 금지 — manifest pin·소비 코드만.
- `ThirdParty/` · `Plugins/` 직접 수정 금지 (어댑터만 `Project/Scripts/ThirdPartyAdapters/`).
- 설계 `.md`는 Assets 밖.

### 프로세스 · 문서

- 7단계: Define → Design → DoD → Build → Verify → Record (실패 시 Recovery).
- 구조 변경 시 Architecture · (크면) Plan. Optimization은 추적 필요할 때만.
- 스모크·QA **제안·실행**은 사용자 요청 전 금지. behavioral SC는 코드 리뷰만으로 pass 금지.
- 커밋은 사용자 **명시 요청** 시에만. `type(scope): 설명`

### 코딩

- Kit common C#·네이밍·포니테일.
- 네임스페이스: 주변·아래 override에 맞춤.

## 이 타이틀 override (채울 것)

| 항목 | 값 |
|------|-----|
| Unity 루트 | `<UnityProjectFolder>/` |
| 게임 스크립트 | 예: `Assets/Project/Scripts/` |
| 문서 루트 | 예: `Docs/<title>/` 또는 `docs/project/` |
| asmdef (Game 등) | `<…>` |
| 공유 Core 패키지 id | `<com.example.core>` (없으면 —) |
| 네임스페이스 루트 | `<…>` |

### 자주 쓰는 경로

- 스테이지/도메인 enum: `<path>`
- Addressables JSON / Scriptable: `<path>`
- 기타: `<…>`

## 링크

- Kit game: `unity-studio-kit/docs/game/README.md`
- 타이틀 문서 허브: `<docs/README.md>`
