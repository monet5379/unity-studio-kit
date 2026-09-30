# 글쓰기 가이드 (Unity Kit)

이 Kit의 `docs/`와 프로젝트 `AGENTS.md`·README를 쓸 때 따르세요.  
토스 [테크니컬 라이팅](https://technical-writing.dev/overview.html)([GitHub](https://github.com/toss/technical-writing))의 **유형 · 정보 구조 · 문장**만 Unity 작업에 맞게 축약했어요. 
사이트 notes·Jekyll 전용 규칙은 여기에 두지 않아요.  
원 가이드 © 2024 Viva Republica, Inc. — [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/). 고지: [`NOTICE`](../../NOTICE).

에이전트 요약: [`.cursor/rules/common/writing-guide.mdc`](../../.cursor/rules/common/writing-guide.mdc)

## 적용 범위

- 이 Kit의 `docs/` · `templates/` 사람용 본문
- `profile: game` 타이틀의 `docs/**` · `Docs/**` · `AGENTS.md`

## 독자 · 톤


|     |                                                         |
| --- | ------------------------------------------------------- |
| 독자  | 몇 달 뒤의 본인, 새 Unity 프로젝트를 붙이는 본인. (에이전트는 `.mdc` 요약을 봐요.) |
| 톤   | **해요체**로 통일. 1인칭 허용. (토스 가이드와 같은 말투 축.)                 |
| 목표  | 규칙을 외우게 하지 않고, **다음에 무엇을 하면 되는지** 바로 알게 해요.             |


Kit `docs/` · README · `templates/` 사람용 본문은 **해요체**로 맞춰 두었어요. 새로 쓰거나 고칠 때도 해요체를 유지하세요. (에이전트 강제 규칙 중 `ponytail` 같은 긴 `.mdc`는 요약 톤을 유지할 수 있어요.)

**톤 예외:** `notes/` · `interview/` (및 타이틀 `AGENTS.md`에 명시한 경로)는 구어체·평서체를 허용해요. Architecture · Optimization · GDD `locked` 본편은 해요체를 유지하세요.

## 정본 사다리 (game 권장)

충돌할 때는 아래 순서로 맞추세요.

```text
코드 ≥ Architecture ≥ 설계 정본
```

설계 정본은 GDD `locked`(또는 Decision), 또는 Technical Design이에요. 타이틀 `AGENTS.md`가 경로를 정해요.

- **코드**가 현재 동작의 최종 정본이에요.
- **Architecture**는 구조·경계·계약의 문서 정본이에요. 코드와 어긋나면 Architecture를 고치거나 코드 변경을 되돌리세요.
- **설계 정본**은 구현 근거로만 쓰고, Architecture·코드보다 우선하지 않아요. GDD는 `locked`(또는 Decision)만 해당해요.

## docs와 rules


|                    | 역할                                       |
| ------------------ | ---------------------------------------- |
| `docs/**`          | **사람용 정본** — lead · 왜 · 예시 · 표           |
| `.cursor/rules/**` | **에이전트용 요약** — Must / Must not + docs 링크 |


내용이 바뀌면 **docs를 먼저** 고치고, rules는 짧은 요약만 맞추세요. 규칙 전문을 `.mdc`에 장문으로 쓰지 마세요.

## 정보 구조

1. **가치를 먼저 (lead)** — 문서 첫 2~4문장에 “이 페이지가 무엇을 결정·가능하게 하는가”를 쓰세요.
2. **개요를 빼지 않기** — 필요하면 lead 다음에 전제·독자·관련 링크를 짧게.
3. **한 페이지 한 주제** — Overview와 AssetsLayout을 한 파일에 합치지 마세요.
4. **예측 가능한 목차** — 아래 유형별 골격을 기본으로, 필요 섹션만 두세요.
5. **제목** — 무엇/왜가 보이게. 부제(`—`)는 쓰지 마세요.

표·불릿은 **스캔용**으로 유지하세요. 표만으로 끝내지 말고, lead나 한두 문장으로 맥락을 주세요.

## 문서 유형 (Kit)

새 문서를 쓰기 전 **주 유형 하나**를 고르세요.


| 유형         | 독자가 얻는 것     | Kit에서                                            |
| ---------- | ------------ | ------------------------------------------------ |
| **시작하기**   | 붙이는 순서       | 루트 README · `templates/`                         |
| **개념**     | 왜 이 프로필·경계인가 | `docs/*/Overview.md`                             |
| **참조**     | 표·금지·경로      | AssetsLayout · Csharp · Shell · Documentation 본문 |
| **How-to** | 단계대로 따라 하기   | (선택) 새 패키지/타이틀 붙이기 한 장                           |
| **프로세스**   | 언제 어떤 산출물인가  | DevelopmentProcess · AgentWorkflow · DocsLite · LocaleDocs(한글 README) |


프로필 문서 무게:


|      | personal                                                                 | game                                                            |
| ---- | ------------------------------------------------------------------------ | --------------------------------------------------------------- |
| 기본   | README + Invariants ([DocsLite](../personal/DocsLite.md))                | Architecture · Plan ([Documentation](../game/Documentation.md)) |
| 충돌 시 | DocsLite가 “문서 최소”를 이김 (README 언어는 [LocaleDocs](../personal/LocaleDocs.md)) | Documentation · DevelopmentProcess가 이김                          |




## 유형별 골격

고정 템플릿이 아니라 **기본 골격**이에요.

### 시작하기 / How-to

1. lead
2. 전제 (Kit 멀티 루트, profile)
3. 단계
4. 확인 (선택)
5. 다음 링크



### 개념 (Overview)

1. lead
2. 대상 / 대상이 아닌 것
3. common 위에 더하는 것 (짧게)
4. 프로젝트에 적는 법
5. 하지 않는 것



### 참조

1. lead (한두 문장)
2. 표·금지·경로
3. 관련 rules / 형제 문서 링크



### 프로세스

1. lead
2. 원칙
3. 단계·표
4. 예외·Recovery



### Architecture (game · 타이틀 repo)

[Documentation.md](../game/Documentation.md)의 **Architecture 작성 규약**(필수 골격 · Refactoring · 작성·갱신)을 따르세요. lead에 “이 기능이 지금 무엇을 보장하는가”를 넣으세요.

## 문장

- **주어를 분명하게** — 독자·작성자·에이전트. 시스템 주어는 동작·경계 설명에만.
- **필요한 정보만** — “~할 수 있어요” 남발 대신 허용/금지를 단정하세요.
- **용어 통일** — `profile`, `common` / `personal` / `game`, `Architecture`, Plan.
- **의도적 범위 제한**은 유지하세요 (`기각`, `이 Kit에 두지 않음`).
- 경로·asmdef·명령은 꾸미지 않고 **참조 톤**으로 적으세요.



## Kit 문서를 고칠 때

1. 유형을 정하세요.
2. lead를 쓰세요.
3. 골격을 채우세요.
4. rules 요약이 있으면 한 단락만 동기화하세요.

루트 README · Overview · templates를 **진입**으로 먼저 맞추고, 참조 문서는 lead만 보강해도 돼요.
