# 문서 (personal · 가볍게)

personal에서는 Architecture·Plan 없이도 계약을 남길 수 있게, **README를 정본**으로 둬요. game 문서 정책을 여기 강제하지 않아요.


**왜 README만인가요?** 
공개 패키지·실험은 설치·불변조건만 있으면 소비자가 바로 이해해요. Plan·Architecture 트리를 기본으로 두면 문서 비용이 이득보다 커져요.


## 기본

- **정본은 README**예요. Architecture / Plan / Optimization 문서는 기본으로 만들지 않아요.
- 계약이 있으면 README에 **Invariants** 절로 적어요. 표·짧은 불릿이면 충분해요.
- 스크린샷·부가 설명만 `docs/`에 둬요. Assets 안에 긴 설계 md를 넣지 않아요.

## 언제 조금만 더 쓰나

| 상황 | 해도 됨 |
|------|---------|
| API·실패 시나리오가 김 | README 절 추가 또는 `docs/` 한 장 |
| 실험 메모 | `docs/notes/` 짧은 md (프로세스 강제 없음) |
| 구조가 커져 타이틀에 가까움 | **game** 프로필로 전환을 검토 |

## README 언어

공개 README 정본은 **한글 `README.md` 하나**예요. 영문·`README.<locale>.md`·언어 셀렉터는 두지 않아요. 상세: [LocaleDocs.md](LocaleDocs.md).

## 에이전트

- 요청 없이 Plan·아키텍처 파일 트리·스프린트 문서를 만들지 않아요.
- 문서 요청이 있으면 README·Invariants를 먼저 갱신해요.
- 큰 구조 변경이어도 personal에서는 “짧은 README 갱신”이 기본이에요.
