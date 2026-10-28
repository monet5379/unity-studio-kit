# <PackageOrProjectName> — Agent Guide

```text
profile: personal
```

공개 패키지·실험용이다. Cursor는 **이 repo + unity-studio-kit** 멀티 루트로 여한다.

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
├── README.md                 ← 한글. Install · Invariants · Out of scope
├── docs/
│   ├── architecture/
│   │   ├── README.md         ← Architecture 허브 (본편 2+일 때)
│   │   └── Architecture_<Feature>.md
│   └── notes/                ← 선택 (짧은 메모)
├── Assets/
│   ├── <PackageName>/        ← 설치·복사 단위
│   └── Demo/                 ← 선택. 놀이터. 비설치
```

## 에이전트가 지킬 것

- Kit **common** + **personal** (README 계약 + `Architecture_*`; Plan/Optimization/ADR는 요청 시만).
- `.meta` 생성·수정·삭제 금지. `ThirdParty/` · `Plugins/` 직접 수정 금지.
- 커밋은 사용자 **명시 요청** 시에만. Kit CommitMessages (`unity-studio-kit/docs/common/CommitMessages.md`) — `type(scope): 한글 제목` + **본문(why) 필수** (영어 필요 시 아래 override)
- Demo를 출시 스키마·필수 설치 경로로 취급하지 않음.

## 이 repo override (선택)

Kit [UnityCliAgent](unity-studio-kit/docs/common/UnityCliAgent.md) — 에이전트 Shell Unity headless 금지. 진입점만 이 repo에 적는다.

| 항목 | 값 |
|------|-----|
| Unity CLI 진입점 | 예: `scripts/verify.ps1` · `—` |
| Unity CLI 정본 문서 | 예: README §verify · `docs/architecture/Architecture_*.md` · — |

## 이 repo만의 메모 (선택)

- Kit와 다른 규약: <항목 — Kit 값을 override> (없으면 —)
- 네임스페이스: `<Namespace>`
- 의존: <예: Newtonsoft.Json>
- 기타: <불변조건 한두 줄 또는 README 링크>

### 커밋 (이 repo)

Kit CommitMessages (`unity-studio-kit/docs/common/CommitMessages.md`)를 따르고, 아래만 이 repo에서 정한다.

| 항목 | 값 |
|------|-----|
| 언어 | 한글 (Kit 기본) · 공개 패키지면 `영어`로 override |
| scope (정본) | 예: `package`, `demo`, `docs`, `ci` |
