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

## 네이밍 (의미)

동사·접두사는 아래 표를 따르세요. 프로젝트에 도메인 delta rule이 있으면 그 규칙이 이 표보다 우선해요. 우선순위는 도메인 delta rule > 이 표 > casing이에요. `Check*` / `Cleanup*` / `Determine*` / `Initialize()` 는 손댄 구간만 맞추고, 일괄 rename은 하지 않아요.

| 대상 | 써요 | 새로 쓰지 않아요 |
|------|------|------------------|
| bool | `Is*` · `Has*` · `Can*` · `Allows*` · `Try*` | `Determine*`, 단순 bool `Check*` / `Validate*` |
| 이벤트 | 수신 `On*`, 이어서 `Handle*` | |
| public API | `Reset*` · `Configure*` · `BindTo*` · `Despawn*` · `Clear*` 등 구체 동사 | 범용 `Initialize()` · `Cleanup*` |
| 코루틴 | `Begin*` · `Run*` · `Stop*` · `Yield*` | 같은 클래스의 `Process*` 오버로드 |
| 여러 대상 | `*All*` 또는 복수형 | |
| 기타 | lazy-init `Ensure*` · 트랜잭션 `Record*` · 콜백 `Register*` / `Unregister*` | `Suicide*` · `Fore*` |

## 프로퍼티

- `{ get; init; }` **사용 금지**. 객체 이니셜라이저로만 채우는 패턴도 쓰지 않아요.
- 불변: 생성자 + `{ get; }`
- 가변: `{ get; set; }`

```csharp
// 금지
public readonly struct Foo
{
    public string Name { get; init; }
}

// 불변
public readonly struct Foo
{
    public Foo(string name) => Name = name;
    public string Name { get; }
}
```

## Unity / C# 관례

- 네임스페이스는 **주변 코드·프로젝트 관례**에 맞추세요.
- Inspector: `[SerializeField] private` (+ 필요 시 읽기 전용 프로퍼티)
- **플레이어 대면** UI 텍스트: `TextMeshProUGUI`만 — 레거시 `UnityEngine.UI.Text` 금지
- **개발·데모 IMGUI** (**선택**, 오버레이 작업 시): [DevImgui.md](DevImgui.md) · personal은 [DemoGui.md](../personal/DemoGui.md)
- 비즈니스·게임 로직 메서드 위: 목적 **한 줄 한국어** 주석 (단순 getter/래퍼는 생략 가능)

## partial class

- base class·interface는 **메인 파일 1곳**에만 선언해요.
- 분할 partial은 `public partial class Foo`만 — 상속 목록 반복 금지예요.
- 동일 타입 partial은 **동일 asmdef·namespace**예요.

## hot path

- `Update` / `FixedUpdate` / 빈번한 루프: LINQ·불필요한 문자열 할당·박싱·반복 `GetComponent<T>()` 금지
- `GetComponent`: `Awake` 또는 지연 캐싱 (`??=`)
