# C#

personal · game 공통 C# 관례예요. 새 코드·수정 구간에 적용하고, 레거시 일괄 rename은 하지 않아요.

Cursor: [`csharp-standards.mdc`](../../.cursor/rules/common/csharp-standards.mdc) · [`naming-semantics.mdc`](../../.cursor/rules/common/naming-semantics.mdc)

## 네이밍 (casing)

| 대상 | 규칙 |
|------|------|
| 타입·메서드·프로퍼티 | PascalCase |
| 인터페이스 | `I` 접두사 |
| private / readonly 필드 | `_camelCase` |
| 지역 변수·매개변수 | camelCase |
| `const` | `UPPER_SNAKE_CASE` |

의미(semantic) 동사·접두사는 [`naming-semantics.mdc`](../../.cursor/rules/common/naming-semantics.mdc).

## 프로퍼티

- `{ get; init; }` **사용 금지**
- 불변: 생성자 + `{ get; }`
- 가변: `{ get; set; }`

## Unity / C# 관례

- 네임스페이스는 **주변 코드·프로젝트 관례**에 맞추세요.
- Inspector: `[SerializeField] private` (+ 필요 시 읽기 전용 프로퍼티)
- UI 텍스트: `TextMeshProUGUI`만 — 레거시 `UnityEngine.UI.Text` 금지
- 비즈니스·게임 로직 메서드 위: 목적 **한 줄 한국어** 주석 (단순 getter/래퍼는 생략 가능)

## partial class

- base class·interface는 **메인 파일 1곳**에만 선언해요.
- 분할 partial은 `public partial class Foo`만 — 상속 목록 반복 금지예요.
- 동일 타입 partial은 **동일 asmdef·namespace**예요.

## hot path

- `Update` / `FixedUpdate` / 빈번한 루프: LINQ·불필요한 문자열 할당·박싱·반복 `GetComponent<T>()` 금지
- `GetComponent`: `Awake` 또는 지연 캐싱 (`??=`)
