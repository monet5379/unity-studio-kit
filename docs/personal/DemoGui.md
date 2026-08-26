# Demo GUI (personal)

**선택** — PackageLayout·DocsLite·README Invariants보다 우선순위가 낮아요. **Demo·F1 오버레이를 만질 때만** 보세요.

공통 역할 원칙은 [DevImgui.md](../common/DevImgui.md), 여기서는 Demo 경계와 권장 기본값을 정해요.

Cursor: [`demo-gui.mdc`](../../.cursor/rules/personal/demo-gui.mdc)  
레이아웃: [PackageLayout.md](PackageLayout.md)

## 대상

- `Assets/Demo/` 의 F1·디버그·시나리오 오버레이 (`OnGUI` / `GUILayout`)
- 패키지 API를 보여 주는 놀이터 UI

## 대상이 아닌 것

- `Assets/<PackageName>/` Runtime·Editor에 넣는 **설치 단위** UI
- 플레이어 대면 Canvas / TMP HUD
- 타이틀 `DeveloperGUI` 프레임워크 전체 이식 (윈도우 드래그·카테고리 탭 등)

## 스타일 역할

| 이름 | 용도 | 권장 기본 |
|------|------|-----------|
| `Title` | 패널 제목, `section_*` 헤더 | Bold, **14**, richText |
| `Content` | 슬롯·상태·본문 줄 | Normal, **12**, wordWrap, richText |
| `Sub` (선택) | 진단 보조·힌트 | Italic 또는 11, Content보다 덜 튀는 색 |
| `Button` | 액션 버튼 | Bold, **14**, MiddleCenter |

색은 프로젝트 자유예요. CreamIvory 같은 타이틀 팔레트를 personal에 강제하지 않아요.

## 구현 힌트

- 오버레이 한 클래스 안에 `EnsureGuiStyles()` 로 캐시하거나, Demo 전용 작은 `*GuiStyles` / `*GuiData` 타입 하나를 둬요.
- 섹션 헤더 → `Title`, 정보·status → `Content`, 클릭 가능 행 → `Button`.
- 창 너비·버튼 크기가 있으면 스타일과 **같은 객체**에 두세요 (`RefreshSize` 패턴).

```csharp
// 개념 예 — 프로젝트 이름·네임스페이스에 맞추세요
_titleStyle = new GUIStyle(GUI.skin.label)
{
    fontStyle = FontStyle.Bold,
    fontSize = 14,
    richText = true,
    wordWrap = true
};
_contentStyle = new GUIStyle(GUI.skin.label)
{
    fontSize = 12,
    richText = true,
    wordWrap = true
};
_buttonStyle = new GUIStyle(GUI.skin.button)
{
    fontStyle = FontStyle.Bold,
    fontSize = 14
};
```

## 규칙

- Demo IMGUI는 **설치 패키지 경로 밖** (`Assets/Demo/`)에만 둬요.
- README에 Demo는 설치하지 않는다고 밝혀 두세요.
- 공통 [DevImgui](../common/DevImgui.md)의 Must not(전역 skin 변조, OnGUI마다 new Style)을 그대로 지켜요.

## 하지 않는 것

- Demo 스타일 헬퍼를 Runtime asmdef에 넣고 소비 게임에 강제하기
- Dragon `TSGUIData` / `TSGUIEx` / Odin / `TSColors` 를 personal Kit 필수로 복사하기
- Title 없이 Content만으로 섹션을 나누기 (스캔이 어려워져요)
