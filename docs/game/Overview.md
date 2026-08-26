# Game 프로필

출시·팀 타이틀은 공유 패키지 경계와 문서·프로세스 무게가 personal과 달라요. 이 문서는 game을 쓸지 정하고, Kit game 문서군으로 들어가기 전에 읽어요.

유틸·실험만이면 [personal Overview](../personal/Overview.md)를 쓰세요.

## 대상

- 캠페인·출시 대상 게임
- 공유 Core UPM + 타이틀 Game asmdef
- Architecture · Plan · 검증 대조가 의미 있는 규모

## 대상이 아닌 것

- 복사형 유틸·짧은 데모만 있는 repo (→ personal)

## common 위에 더하는 것

| | personal | game |
|---|----------|------|
| 문서 | README + Invariants | Architecture / Optimization · Plan |
| 프로세스 | ponytail 위주 | 7단계 (Define→Record, 실패 시 Recovery) |
| Assets | 복사 단위 + Demo | `Project/` · Addressables · Tier |
| 공유 패키지 | 복사·단독 | manifest pin · 소스 직접 수정 금지 |

## 프로젝트에 적기

```text
profile: game
```

템플릿: [`templates/AGENTS.game.md`](../../templates/AGENTS.game.md)  
타이틀 전용 경로·도메인은 **이 게임 repo**의 `AGENTS.md` · `.cursor/rules/<title>/`에만 두세요.

## Kit에 두는 것 / 안 두는 것

| 이 Kit (game) | 타이틀·프레임워크 repo |
|---------------|------------------------|
| Assets 표준 · Tier 원칙 · 문서 정책 · 7단계 | 타이틀 enum·경로 override |
| Cursor game 규칙 요약 | 프레임워크 Architecture 본편·배포 태그 전문 |

다음: [AssetsLayout.md](AssetsLayout.md) · [Documentation.md](Documentation.md) · [DevelopmentProcess.md](DevelopmentProcess.md)
