# 패키지 레이아웃 (personal)

공개·실험 repo에서 **무엇을 복사 설치 단위로 둘지**를 정해요. 타이틀용 `Project/` · Addressables는 game 프로필이에요.

## 권장 트리

```text
<repo>/
├── README.md              ← Install · Invariants · Out of scope
├── LICENSE
├── AGENTS.md              ← profile: personal (선택)
├── Assets/
│   ├── <PackageName>/     ← 복사·설치 단위 (Runtime / Editor)
│   └── Demo/              ← 선택. 놀이터만. 설치 대상 아님
└── docs/                  ← 선택. 스크린샷·짧은 메모
```

## 규칙

- **설치 단위**는 `Assets/<PackageName>/` 한 덩어리예요. asmdef가 있으면 유지한 채 복사해요.
- **`Assets/Demo/`** 는 참고·재생용이에요. README에 “Demo는 설치하지 않음”을 밝혀 주세요.
- Demo에 출시 스키마·도메인 enum·타이틀 전용 래퍼를 넣지 마세요. 필요하면 소비 쪽 게임에 둬요.
- 벤더 `ThirdParty/` · `Plugins/` 는 직접 수정하지 마세요 (common과 동일).
- `.meta` 는 Unity가 관리해요 (common과 동일).

## README에 넣을 최소 항목

1. 한 줄 목적  
2. Install (무엇을 어디에 복사하는지)  
3. Invariants (깨면 안 되는 계약)  
4. Out of scope  

상세: [DocsLite.md](DocsLite.md)
