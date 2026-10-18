# 개발용 IMGUI

**선택** — 출시 UI·패키지 Invariants·C# 공통 규칙보다 우선순위가 낮다. F1·Developer 등 **개발·데모 IMGUI를 만질 때만** 본다.

역할별 스타일을 한곳에서 맞추기 위한 공통 원칙이다. 플레이어 대면 uGUI(TMP·Canvas)는 [Csharp.md](Csharp.md)를 본다.

Cursor: [`dev-imgui.mdc`](../../.cursor/rules/common/dev-imgui.mdc)  
personal Demo: [DemoGui.md](../personal/DemoGui.md)

## 왜 나누는가

IMGUI 기본 skin만 쓰면 제목·본문·버튼이 같은 크기로 보인다. 스타일을 호출마다 새로 만들거나 `GUI.skin`을 직접 고치면 화면마다 들쭉날쭉해진다. **역할 → 스타일**을 고정하면 스캔하기 쉽고, 프로젝트 간에 읽히는 느낌이 비슷해진다.

## 역할

| 역할 | 쓰는 곳 | 기본 감각 |
|------|---------|-----------|
| **Title** | 패널·섹션 헤더 | Bold, Content보다 큼, richText 허용 |
| **Content** | 상태·목록·본문 | Normal, wordWrap, richText 허용 |
| **Sub** (선택) | 보조 설명·힌트 | Content보다 작거나 italic, 덜 튀는 색 |
| **Button** | 액션 | Bold, 가운데 정렬 |

숫자는 프로젝트가 정한다. 공통은 **계층**만 강제한다. (참고 기본값 예: Title 14 · Content 12 · Sub 11 · Button 14)

## 규칙

- 스타일·버튼/창 크기는 **한 객체 또는 한 `Ensure*Styles`** 에서만 만든다.
- `OnGUI`마다 `new GUIStyle(...)` 를 반복하지 않는다. 캐시하거나 `RefreshStyle` 한 번으로 둔다.
- Label/Button을 그릴 때 **역할에 맞는 스타일**을 넘기한다. skin 기본값에만 기대지 않는다.
- 플레이어 HUD·팝업 등 **출시 UI**에 IMGUI 스타일 규칙을 적용하지 않는다. 그쪽은 TMP / Canvas이다.
- 개발 전용 GUI는 에디터·Development 빌드에서만 켜는 패턴을 권장한다. (강제 매크로는 프로젝트 몫)

## 하지 않는 것

- `GUI.skin.label` 등을 전역으로 직접 변조해 다른 창까지 바꾸기
- Title/Content를 한 스타일로 퉁치기
- 이 문서를 uGUI·TMP·로컬라이제이션 파이프라인 정본으로 쓰기
