# 커밋 메시지

personal · game 공통으로, [Conventional Commits](https://www.conventionalcommits.org/) 형식과 **제목·본문 작성법**을 맞춰요.  
프로젝트마다 다른 **scope 목록·언어 override·패치노트 경로**는 이 문서에 두지 않고, 각 repo `AGENTS.md`에 적어요.

에이전트 요약: [`.cursor/rules/common/commit-messages.mdc`](../../.cursor/rules/common/commit-messages.mdc)  
최소 Git 규칙: [UnityBasics.md](UnityBasics.md)

---

## 형식

```text
<type>(<scope>): <제목>

[본문 — 선택]

[Footer — 선택]
```

- 제목은 **권장 50자 전후, 최대 72자**.
- `scope`는 선택이에요. 변경 영역이 분명할 때만 붙이에요.
- 본문은 필요할 때만 써요. **왜** 바꿨는지를 1–2문장으로 적어요.
- 커밋은 사용자가 **명시적으로 요청할 때만** 만들어요. ([UnityBasics](UnityBasics.md))

---

## Type

| type | 언제 쓰나 |
|------|-----------|
| `feat` | 사용자에게 보이는 기능·동작 추가 |
| `fix` | 버그 수정 |
| `docs` | 문서만 변경 (README, 설계·가이드 등) |
| `style` | 동작 변화 없는 포맷·들여쓰기·이름만의 정리 |
| `refactor` | 동작은 같지만 구조·가독성 개선 |
| `perf` | 성능 개선 |
| `test` | 테스트 추가·수정 |
| `chore` | 빌드·설정·잡무 (기능 변경 아님). CI는 보통 `chore(ci):` |

한 커밋에 성격이 섞이면 **주된 의도**의 type 하나를 고르세요.  
예: 기능 추가 + 문서 갱신이면 `feat`, 문서만이면 `docs`.

---

## Scope

디렉터리·영역 기준으로 짧게 쓰세요. **허용 scope 목록은 프로젝트 `AGENTS.md`가 정본**이에요.

Kit에서는 예시만 둡니다. 애매하면 scope를 생략해도 돼요.

| 예시 scope | 대상 (예시) |
|------------|-------------|
| `ui` | 화면·입력 위주 UI |
| `save` | 저장·슬롯 |
| `docs` | `docs/` · README |
| `ci` | GitHub Actions 등 |
| `common` | Kit·공유 공통 영역 |

```text
fix: 타이틀 복귀 시 페이즈가 꼬이던 문제 수정
```

---

## 제목 · 언어

**기본은 한글**이에요. 제목·설명 문장은 한글로 쓰고, 코드명·API·로그 문구는 영어 그대로 둬도 돼요.

공개 패키지 등에서 영어 커밋이 필요하면 프로젝트 `AGENTS.md`에서 언어를 override하세요.

- **무엇을/왜**가 한 줄로 드러나게 쓰세요.
- 명령형·간결한 서술형 모두 허용해요. 예: `…을 추가`, `…을 수정`, `…을 단축`
- 문장 끝에 마침표를 붙이지 마세요.
- 제목에 `v0.1.30:` 같은 **버전 접두어는 쓰지 마세요.** 버전은 패치노트·본문·태그·릴리스 산출물로 표현하세요.

과거 영어(또는 다른 언어) 커밋은 그대로 둡니다. **이 규칙을 쓴 뒤부터** 위 형식을 따르세요.

---

## 본문 · Footer (선택)

제목만으로 이유가 안 드러날 때 본문을 쓰세요.

- **why** 중심 (파일 나열·diff 요약은 피해요)
- 빈 줄로 제목과 본문을 구분해요
- Breaking change가 있으면 본문 또는 footer에 `BREAKING CHANGE:`로 명시해요
- 이슈 닫기는 footer 예: `Closes #12`

---

## 예시 (공용)

```text
feat(ui): 설정 화면에서 슬롯 이름을 바꿀 수 있게 함

빈 이름은 저장하지 않고 이전 값을 유지한다.
```

```text
fix(save): 슬롯 복사 후 메타 GUID가 겹치던 문제 수정
```

```text
docs: 커밋 메시지 공용 규칙 문서 추가
```

```text
chore(ci): 테스트 job에 Unity 버전 매트릭스 추가

로컬과 CI 버전 불일치를 줄인다.
```

```text
refactor(save): 백업 경로 조합을 한 헬퍼로 모음
```

---

## 하지 않을 것

- `update`, `수정`, `워킹`처럼 내용이 없는 제목
- Kit 기본(한글)을 쓰는데 제목·설명을 **영어만**으로 쓰기 — `AGENTS`에서 영어 override한 repo는 제외
- 한 커밋에 서로 무관한 대형 변경을 섞기 (가능하면 나눔)

---

## Kit에 두지 않는 것

아래는 **이 Kit 정본에 넣지 마세요.** 타이틀·패키지마다 달라요.

| 두지 않음 | 이유 |
|-----------|------|
| 프로젝트 전용 scope 표 (`prototype`, `launcher`, `ai` 등) | repo 레이아웃에 종속 |
| 패치노트 경로·internal/external 워크플로 | 릴리스/문서 프로세스 |
| 특정 게임·패키지 도메인 예시 (페이즈명, `serve.py` 등) | 공용 예시로 일반화하거나 프로젝트 docs에 |
| commitlint / CI 강제 설정 | 필요할 때 각 repo에서 |

---

## 프로젝트에 둘 것

각 소비 repo의 `AGENTS.md`(또는 타이틀 docs)에 적어 두세요. 템플릿: [`templates/AGENTS.game.md`](../../templates/AGENTS.game.md) · [`templates/AGENTS.personal.md`](../../templates/AGENTS.personal.md)

```text
## 커밋 (이 repo)

- Kit: unity-studio-kit `docs/common/CommitMessages.md`를 따른다.
- 언어: 한글 (Kit 기본) | 영어   ← 하나만
- scope (정본): <짧은 표 — 예: ui, save, docs, ci>

(선택) 패치노트·버전 표기 경로: <docs/…>
```

에이전트·사람은 **형식·type·작성법**은 Kit를, **scope·언어·패치노트**는 이 표만 보면 돼요.

---

## 강제 도구

commitlint 등 강제 도구는 Kit에 두지 않아요. 규칙 위반이 잦아지면 **그 프로젝트**에서 검토하세요.  
넣을 때 scope enum 강제는 비추천이에요 (생략·확장이 잦음).

---

## 참고

- 스펙: [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/)
- Git 최소: [UnityBasics.md](UnityBasics.md)
