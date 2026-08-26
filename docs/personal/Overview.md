# Personal 프로필

공개 유틸 패키지나 짧은 Unity 실험에는 **가벼운 규칙**만 필요해요. 이 문서는 personal을 고를지, game으로 올릴지 정할 때 읽어요.

출시 타이틀·팀 Plan·Architecture가 필요하면 [game Overview](../game/Overview.md)로 가세요.

## 대상

- 복사해 쓰는 유틸 패키지
- 프로토타입·데모 씬으로 API를 보여 주는 작은 repo

## 대상이 아닌 것

- 출시·캠페인 타이틀 (→ game)
- 팀 스프린트 Plan이 기본인 작업

## common 위에 더하는 것

| | personal | game |
|---|----------|------|
| 문서 | README + Invariants | Architecture / Plan |
| 프로세스 | ponytail·최소 diff | 7단계·Record |
| 레이아웃 | `Assets/<Package>/` + 선택 Demo | `Project/` · Addressables |
| Plan | 기본 불필요 | 구조 변경 시 |

## 프로젝트에 적기

`AGENTS.md` 상단:

```text
profile: personal
```

템플릿: [`templates/AGENTS.personal.md`](../../templates/AGENTS.personal.md)  
Kit를 멀티 루트로 연 경우 personal 규칙은 `alwaysApply`가 아니에요. 에이전트는 `docs/personal`과 `.cursor/rules/personal`을 따르세요.

## 하지 않는 것

- 팀 스프린트 Plan·Architecture를 personal에 강제하지 않아요.
- 타이틀 전용 경로·도메인을 이 Kit personal에 모으지 않아요.
- Demo를 출시 스키마·필수 설치 경로로 취급하지 않아요.
- 패키지 UI 언어 전환 구현(스크립트·Prefs·메뉴)을 Kit에 두지 않아요. [LocaleDocs](LocaleDocs.md)는 README 파일 로케일만이에요.

다음: [PackageLayout.md](PackageLayout.md) · [DocsLite.md](DocsLite.md) · (선택) [DemoGui.md](DemoGui.md) · [LocaleDocs.md](LocaleDocs.md)
