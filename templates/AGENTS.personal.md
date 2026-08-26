# <PackageOrProjectName> — Agent Guide

```text
profile: personal
```

공개 패키지·실험용이에요. Cursor는 **이 repo + unity-studio-kit** 멀티 루트로 여세요.

| Kit | 경로 |
|-----|------|
| 공통 | `unity-studio-kit/docs/common/` · `.cursor/rules/common/` |
| 글쓰기 | `unity-studio-kit/docs/common/WritingGuide.md` |
| 프로필 | `unity-studio-kit/docs/personal/` · `.cursor/rules/personal/` |

## 프로젝트 개요

- **목적:** <한 줄>
- **Git 루트:** 이 저장소 최상단
- **Unity:** `<UnityProjectFolder>/` (에셋은 여기만) — 루트와 동일하면 `./`

## 레이아웃

```text
<repo>/
├── AGENTS.md
├── README.md                 ← Install · Invariants · Out of scope
├── README.<locale>.md        ← 선택. 다국어 (LocaleDocs)
├── Assets/
│   ├── <PackageName>/        ← 설치·복사 단위
│   └── Demo/                 ← 선택. 놀이터. 비설치
└── docs/                     ← 선택 (스크린샷·짧은 메모)
```

## 에이전트가 지킬 것

- Kit **common** + **personal** (Plan/Architecture 기본 불필요, README 정본).
- `.meta` 생성·수정·삭제 금지. `ThirdParty/` · `Plugins/` 직접 수정 금지.
- 커밋은 사용자 **명시 요청** 시에만. 형식: `type(scope): 설명`
- Demo를 출시 스키마·필수 설치 경로로 취급하지 않음.

## 이 repo만의 메모 (선택)

- 네임스페이스: `<Namespace>`
- 의존: <예: Newtonsoft.Json>
- 기타: <불변조건 한두 줄 또는 README 링크>
