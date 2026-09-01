# README 언어 (personal · 한글)

공개 패키지 README는 **한글 `README.md` 하나**가 정본이에요. GitHub 랜딩도 이 파일만 보여 줘요. 영문·다른 locale 파일·언어 셀렉터는 두지 않아요. 문서 무게에서는 [DocsLite](DocsLite.md)가 이깁니다.

## 이 문서가 아닌 것

에디터·F1·인게임 **UI 언어 전환**(Prefs·메뉴·표시 문자열)은 범위 밖이에요. 이 문서는 **README 파일 언어**만 다뤄요. Kit는 그 UI 구현·스크립트 템플릿을 제공하지 않아요.

## 원칙

1. **정본은 `README.md`**, 본문은 **한글**이에요.
2. **한 파일에 영·한 병기**하지 않아요.
3. **`README.<locale>.md`(예: `README.ko.md`, `README.en.md`)를 만들지 않아요.** 영문본을 별도로 두지 않아요.
4. **언어 셀렉터**를 README 상단에 두지 않아요.
5. 코드·식별자·경로·asmdef·명령·로그 문자열은 **영어 유지**해도 돼요. 산문·절 설명만 한글이에요.

## 해요 / 하지 않아요

| 해요 | 하지 않아요 |
|------|-------------|
| `README.md`에 한글 Install · API · Invariants · Out of scope | 영문 `README.md`를 랜딩 정본으로 두기 |
| 식별자·코드 블록은 영문 그대로 | `README.en.md` / `README.ko.md` 등 locale 파일 |
| 공개면만 문서로 유지 | notes·내부 메모까지 영문으로 병행 |
| | 상단 `**English** \| 한국어` 셀렉터 |

## AI 보조 산문 고지

AI로 쓴 한글 산문이 있으면 **그 README 하단**(License 근처)에 한 줄로 밝혀요. 사람이 검수·다듬은 뒤에는 지우거나 “reviewed”로 바꿉니다.

권장 문구:

```markdown
일부 산문은 AI 보조로 작성했어요. 표현이 코드와 어긋나면 코드를 우선해요.
```

## 에이전트

- personal 공개 README를 쓰거나 고칠 때는 **한글 `README.md`만** 갱신해요.
- locale 파일·영문 README·셀렉터를 **새로 만들지 않아요.**
- 문서 최소에서는 [DocsLite](DocsLite.md)가 이깁니다.
