# 문서 (personal)

personal 공개 패키지·실험 repo는 **README 계약**과 **Architecture 본편**을 나눈다. Architecture **파일 형식·골격**은 [game Documentation — Architecture 작성 규약](../game/Documentation.md#architecture-작성-규약)과 같다. Plan·Optimization·ADR·GDD는 game 기본이며 personal에는 **요청 없이 만들지 않는다**.

**왜 나누는가:** GitHub 랜딩 README는 설치·불변조건·범위 밖만 빠르게 읽히게 두고, 구조·흐름·타입·변경 가이드는 `Architecture_*`에 모아 **코드와 함께 갱신**한다.

## 정본 사다리

```text
코드 ≥ Architecture (구조·흐름) ≥ README (Install · Invariants · Out of scope)
```

- **README** — 소비자·clone 직후 계약. 불변조건 전문은 README에 둔다.
- **Architecture** — 현재 구조·경계·흐름·변경 가이드. README에 긴 API·부트 순서·표를 **복사하지 않는다** — Architecture로 링크한다.
- 코드와 Architecture가 어긋나면 **코드가 이김** (game [위키 계약](../game/Documentation.md#에이전트-위키-계약)과 동일).

## 기본 산출물

| 산출물 | 경로 (관례) | personal |
| --- | --- | --- |
| README | repo 루트 `README.md` | **필수** — Install · Invariants · Out of scope |
| Architecture 허브 | `docs/**/architecture/README.md` | 본편 2개 이상이면 **필수** |
| Architecture 본편 | `docs/**/architecture/Architecture_<Feature>.md` | **필수** (기능·모듈당 1파일) |
| Optimization | `optimization/Optimization_*.md` | 추적 필요할 때만 |
| Plan · ADR · GDD | `plan/` · `adr/` · `gdd/` | game — personal 기본 없음 |

한 기능만 있는 작은 실험이면 `Architecture_<Package>.md` **한 장** + README로 충분하다. 본편이 늘면 허브 README 목차를 맞춘다.

## README

- [LocaleDocs](LocaleDocs.md) — 한글 `README.md` 하나.
- 계약은 **Invariants** (또는 **불변조건**) 절 — 표·짧은 불릿.
- 구조 설명·타입 표·시퀀스는 Architecture에 두고 README는 **한 줄 + 링크**.

## Architecture

- 제목 `# Architecture: <Feature>`, 소제목 `## 한글 (English)`, 섹션 아래 *이탤릭 목적 한 줄* — [game Documentation](../game/Documentation.md#architecture-작성-규약) 전문.
- Architecture 본편에 Phase·주차·티켓 이력을 넣지 않는다.
- `Assets/` 안 긴 설계 md 금지 — `docs/`만.

## 에이전트

- **구조·경계·공개 API·부트/로드 흐름**을 바꾸면 해당 `Architecture_*`를 갱신한다. 계약(불변조건)이 바뀌면 **README 먼저**.
- 요청 없이 Plan·Optimization·ADR 트리·스프린트 Record를 만들지 않는다.
- 새 패키지·공개 repo를 문서화할 때 README + `docs/architecture/Architecture_*.md` (+ 필요 시 허브 README)를 **기본 세트**로 둔다.
