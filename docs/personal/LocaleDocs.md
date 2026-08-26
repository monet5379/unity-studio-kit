# 다국어 README (personal · 선택)

공개 패키지 README를 영문과 **다른 언어**로 보여줄 때 이 문서를 읽어요. GitHub는 locale을 자동으로 바꾸지 않아요. 그래서 **별도 파일**과 상단 **언어 링크**로 전환해요. 필수는 아니에요. 문서 무게에서는 [DocsLite](DocsLite.md)가 이깁니다.

## 이 문서가 아닌 것

에디터·F1·인게임 **UI 언어 전환**(Prefs·메뉴·표시 문자열)은 범위 밖이에요. 이 문서는 **README 파일 로케일**만 다뤄요. Kit는 그 UI 구현·스크립트 템플릿을 제공하지 않아요.

## 원칙

1. **한 파일 한 언어**예요. 한 README에 두 언어를 섞지 않아요. ([ppt-skills](https://github.com/CacinieP/ppt-skills/commit/5986d74ae9292b4868f4bc6bf8a63abf289b1fb2)처럼 이중언어 README를 파일로 나눈 선례를 따릅니다.)
2. **정본은 하나**예요. 공개 패키지는 보통 `README.md`(영문)가 정본이에요.
3. **공개면만** 번역해요. Install · API · Invariants · Out of scope. `docs/notes/` 같은 메모는 번역하지 않아요.
4. **구조는 동일**하고, **산문만** 번역해요. 절 제목·표 열 구성·코드 블록은 맞춥니다.

## 파일 이름 · 배치

루트에 두는 기본 패턴이에요.

| 파일 | 언어 |
|------|------|
| `README.md` | 정본 (보통 영문) |
| `README.ko.md` | 한국어 |
| `README.ja.md` | 日本語 |
| `README.zh-CN.md` | 简体中文 |

로케일 태그는 [BCP 47](https://www.rfc-editor.org/info/bcp47)을 씁니다 (`ko`, `ja`, `zh-CN`).

다른 배치: `docs/i18n/README.<locale>.md`도 가능해요. 다만 **번역 랜딩으로 맨 `docs/README.md`만 두지 마세요.** Kit·프로필 목차와 섞입니다.

| 해요 | 하지 않아요 |
|------|-------------|
| `README.md` + `README.<locale>.md` | 한 파일에 영문·한국어 병기 |
| 상단에 언어 셀렉터 링크 | locale 자동 전환을 GitHub에 기대 |
| 공개면(Install·API·Invariants·Out of scope)만 번역 | notes·내부 메모까지 번역 |
| 정본과 같은 절 구조 | 언어마다 다른 목차·절 순서 |
| 요청이 있을 때만 locale 추가 | 요청 없이 번역 파일 생성 |
| AI 번역이면 해당 README 하단에 한 줄 고지 | 셀렉터 옆에 AI 배지·긴 면책 |

## 언어 셀렉터

각 README **맨 위**에 현재 언어를 굵게, 다른 언어는 링크로 두어요.

`README.md` (영문 정본):

```markdown
**English** | [한국어](README.ko.md) | [日本語](README.ja.md)
```

`README.ko.md`:

```markdown
[English](README.md) | **한국어** | [日本語](README.ja.md)
```

`docs/i18n/`에 두면 상대 경로만 맞추면 돼요. 셀렉터 형식 참고: [language-selector-reference](https://github.com/xixu-me/skills/blob/main/skills/readme-i18n/references/language-selector-reference.md).

## 번역 / 비번역

| 번역해요 | 번역하지 않아요 |
|----------|-----------------|
| Install · Quick start | 코드·식별자·경로·asmdef 이름 |
| API 설명 산문 | 명령·로그·에러 문자열(계약이면 원문 유지) |
| Invariants · Out of scope | `docs/notes/` · 실험 메모 |
| 라이선스·고지 **설명** 문장 | LICENSE 본문·NOTICE 전문(필요 시 링크) |

## 동기화

- 정본 계약(Install·Invariants·Out of scope)이 바뀌면 **같은 변경**을 locale에도 반영해요.
- 사용자가 요청하기 전에 locale 파일을 **새로 만들지 않아요.**
- 선택: locale 파일 상단에 HTML 주석으로 정본 커밋 sha를 남겨 동기화 기준을 표시할 수 있어요.

```html
<!-- source: README.md @ <sha> -->
```

## AI 보조 번역 고지

AI로 옮긴 산문이 있으면 **그 언어 README 하단**(License 근처)에 한 줄로 밝혀요. 셀렉터·배지 옆에는 두지 않아요. 사람이 검수·다듬은 뒤에는 고지를 지우거나 “reviewed”로 바꿉니다. 다른 언어 README에 같은 말을 반복하지 않아도 돼요.

권장 문구 (영문 README 예):

```markdown
English prose may be AI-assisted. If wording conflicts, prefer the [Korean README](README.ko.md) or the code.
```

의미 충돌 시 무엇을 믿을지(다른 locale · 코드)를 한 줄에 같이 적어요. 랜딩 파일은 영문이어도, AI 1차 번역이면 검수 전까지 원문 locale·코드를 우선한다고 적어도 됩니다.

## 에이전트

- 다국어 README는 **사용자가 요청할 때만** 만들거나 갱신해요.
- AI로 locale·영문 산문을 쓰면 해당 파일 하단에 **AI-assisted 고지**를 넣어요 (위 절).
- 문서 최소에서는 [DocsLite](DocsLite.md)가 이깁니다. locale은 선택이에요.

## 참고

- [How to localize a README file (GitHub)](https://blog.laratranslate.com/how-to-localize-a-readme-file-github/)
- [Add multiple README on a GitHub repo](https://www.codestudy.net/blog/add-multiple-readme-on-github-repo/)
- [readme-i18n skill](https://github.com/xixu-me/skills/blob/main/skills/readme-i18n/SKILL.md)
- [language-selector-reference](https://github.com/xixu-me/skills/blob/main/skills/readme-i18n/references/language-selector-reference.md)
- [open-design TRANSLATIONS.md](https://github.com/nexu-io/open-design/blob/main/TRANSLATIONS.md)
- [ant-design](https://github.com/ant-design/ant-design) (다국어 README 관행)
- [spec-kit PR #3740](https://github.com/github/spec-kit/pull/3740)
- [duoreadme](https://github.com/duoreadme/duoreadme)
- [readme-generator](https://github.com/nanolaba/readme-generator)
- [readme-i18n-sentinel](https://github.com/sugurutakahashi-1234/readme-i18n-sentinel)
- [ppt-skills: bilingual README split](https://github.com/CacinieP/ppt-skills/commit/5986d74ae9292b4868f4bc6bf8a63abf289b1fb2)
