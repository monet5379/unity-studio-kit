# unity-studio-kit

Unity 프로젝트를 열 때마다 규칙을 복사하지 않도록, **공통 Cursor 규칙과 가이드를 한곳에 모아 두는 Kit**예요. 작업 중인 게임·패키지 repo와 이 저장소를 워크스페이스에 같이 두면, 에이전트와 본인이 같은 기준을 써요.

문서 문체·목차: [`docs/common/WritingGuide.md`](docs/common/WritingGuide.md)

## 이 Kit로 하는 일 / 안 하는 일

| 하는 일 | 안 하는 일 |
|---------|------------|
| AI 규칙(`.cursor`), 공통·프로필 가이드(`docs/`), Cursor skill(`.cursor/skills/`), 새 프로젝트 `AGENTS` 템플릿 | Unity 런타임 코드, UPM 패키지 소스 |
| personal / game 프로필별 **재사용 규약** | 웹 사이트용 글쓰기 규칙 |
| | 타이틀 전용 경로·도메인 규칙 (각 게임 repo에 둠) |
| | 패키지 UI 언어 전환 구현 (에디터·F1·인게임 Prefs·메뉴·문자열). personal [LocaleDocs](docs/personal/LocaleDocs.md)는 README 파일만 |

## 프로필 고르기

규칙은 세 층이에요. **common은 항상** 쓰고, personal과 game 중 **하나만** 고르세요.

| 층 | 언제 | 문서 무게 |
|----|------|-----------|
| **common** | 모든 Unity 작업 | `.meta`, C#, ponytail, Shell, 커밋 |
| **personal** | 공개 패키지·실험·데모 | README + Invariants |
| **game** | 출시·팀 타이틀 | Architecture · Plan · 7단계 |

프로젝트 루트 `AGENTS.md`에 적어요.

```text
profile: personal   # or game
```

자세한 차이: [`docs/personal/Overview.md`](docs/personal/Overview.md) · [`docs/game/Overview.md`](docs/game/Overview.md)

## 시작하기

1. 이 저장소를 clone해요.  
2. [`templates/`](templates/README.md)에서 프로필에 맞는 `AGENTS.*.md`를 프로젝트 루트에 `AGENTS.md`로 복사하고 `<…>`를 채워요.  
3. Cursor에서 **프로젝트 + unity-studio-kit**을 멀티 루트로 열어요.

```text
<workspace>/
├── MyUnityProject/
└── unity-studio-kit/
```

- Kit의 `common` + 선택한 프로필 문서를 따르세요.  
- 타이틀 전용 규칙은 프로젝트 쪽 `.cursor/rules/<title>/`에만 둬요.  
- 나중에 버전 pin이 필요하면 submodule + junction으로 `common`과 해당 프로필만 붙일 수 있어요.

## 구조

```text
unity-studio-kit/
├── docs/common|personal|game/
├── .cursor/
│   ├── rules/common|personal|game/
│   └── skills/         ← Cursor Agent skill (리뷰·Design·DOTS)
└── templates/          ← AGENTS 복사본
```

`common` 중 기본·스코프·포니테일·Shell은 `alwaysApply`. C#·네이밍·글쓰기는 glob.  
personal / game은 `alwaysApply: false` — `profile:`에 맞는 것만 따르세요.

| 문서 | 링크 |
|------|------|
| 글쓰기 | [WritingGuide](docs/common/WritingGuide.md) |
| 공통 | [docs/common](docs/common/README.md) |
| personal | [docs/personal](docs/personal/README.md) |
| game | [docs/game](docs/game/README.md) |
| 템플릿 | [templates](templates/README.md) |
| 리뷰 skill | [`.cursor/skills/code-review`](.cursor/skills/code-review/SKILL.md) — Standards / Spec 두 축 |
| Design 어휘 | [`.cursor/skills/codebase-design`](.cursor/skills/codebase-design/SKILL.md) |
| 아키텍처 스캔 | [`.cursor/skills/improve-codebase-architecture`](.cursor/skills/improve-codebase-architecture/SKILL.md) — **호출 전용** |
| DOTS skill | [`.cursor/skills/unity-ecs-patterns`](.cursor/skills/unity-ecs-patterns/SKILL.md) |

스킬은 해당 요청·단계에서만 켜요 (규칙 alwaysApply 아님). game Design·Verify static은 [DevelopmentProcess](docs/game/DevelopmentProcess.md).  
DOTS·Entities는 위 DOTS skill을 쓰고, hybrid·system group·Entities pin은 **타이틀** `Architecture_*` / `AGENTS.md`가 이깁니다.

## License

[MIT](LICENSE) © 2026 Seunghyeon

제3자 ([`NOTICE`](NOTICE)):
- 포니테일 — [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) (MIT)
- 글쓰기 가이드 — [toss/technical-writing](https://github.com/toss/technical-writing) (CC BY-NC-SA 4.0)
- DOTS skill — [wshobson/agents — unity-ecs-patterns](https://github.com/wshobson/agents/tree/main/plugins/game-development/skills/unity-ecs-patterns) (MIT)
- 리뷰·Design·아키텍처 스킬 — [mattpocock/skills](https://github.com/mattpocock/skills) (MIT)
