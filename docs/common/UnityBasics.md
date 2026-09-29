# Unity 기본

personal · game 공통으로, 에셋·워크스페이스·커밋에서 **항상 지키는 최소 규칙**이에요. 

세부 C#은 [Csharp.md](Csharp.md), 삭제는 [ShellSafety.md](ShellSafety.md)를 보세요.

## 에셋

- `.meta` 생성·수정·삭제 금지 — Unity 에디터가 관리해요.
- 씬·프리팹·ScriptableObject GUID를 임의로 바꾸지 마세요.
- 설계·프로세스 `.md`는 `Assets/` 밖(`docs/` 등)에 둬요. Assets 안 README는 짧은 안내만.

## 씬·프리팹 정본

씬·프리팹·UI Canvas·Inspector `[SerializeField]` 배선의 정본은 Unity 에디터가 저장한 YAML이에요. 그 배선을 에디터 스크립트로 대신 만들지 않아요.

`Assets/**/Editor/`는 **검증·빌드 설정·에셋 임포트**만 담당해요. 씬·프리팹·GameObject를 생성·수정·배선하는 Setup 스크립트는 두지 않아요.

- 금지: `new GameObject` · `AddComponent`로 콘텐츠를 만듦, `SerializedObject`로 Inspector 참조 주입, `[InitializeOnLoad]` 자동 배선, Setup 메뉴로 씬·프리팹 bootstrap
- 누락은 **런타임 스크립트 + 수동 씬 배치**로 채워요. Validator가 있으면 **읽기만** 하고, 실패 메시지로 빠진 배선을 알려요.
- 허용: `AssetPostprocessor` 등 임포트, Build Settings 등록(씬 내용은 바꾸지 않음), 읽기 전용 검증, Plan·ADR에 **1회**라고 적은 마이그레이션

## 워크스페이스

- Git 저장소 **루트**를 Cursor 워크스페이스로 열어요. Unity 하위 폴더만 열지 마세요.
- 이 Kit를 쓸 때는 프로젝트 repo와 `unity-studio-kit`을 멀티 루트로 열어요. ([README](../../README.md))

## Git / 커밋

- 커밋은 사용자가 **명시적으로 요청할 때만** 해요.
- 형식: `<type>(<scope>): <description>` — `feat`, `fix`, `docs`, `refactor`, `test`, `chore`
- 예: `feat(save): 슬롯 백업 경로 분리`, `docs(common): Unity 기본 보강`
- 요청 없이 `git config` 변경·force push·hard reset 등 파괴적 git 명령을 쓰지 마세요.



## 관련 규칙

- `[.cursor/rules/common/unity-basics.mdc](../../.cursor/rules/common/unity-basics.mdc)`
- Shell 삭제: [ShellSafety.md](ShellSafety.md)

