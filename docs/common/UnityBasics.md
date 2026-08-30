# Unity 기본

personal · game 공통으로, 에셋·워크스페이스·커밋에서 **항상 지키는 최소 규칙**이에요. 세부 C#은 [Csharp.md](Csharp.md), 삭제는 [ShellSafety.md](ShellSafety.md)를 보세요.

## 에셋

- `.meta` 생성·수정·삭제 금지 — Unity 에디터가 관리해요.
- 씬·프리팹·ScriptableObject GUID를 임의로 바꾸지 마세요.
- 설계·프로세스 `.md`는 `Assets/` 밖(`docs/` 등)에 둬요. Assets 안 README는 짧은 안내만.

## 워크스페이스

- Git 저장소 **루트**를 Cursor 워크스페이스로 열어요. Unity 하위 폴더만 열지 마세요.
- 이 Kit를 쓸 때는 프로젝트 repo와 `unity-studio-kit`을 멀티 루트로 열어요. ([README](../../README.md))

## Git / 커밋

- 커밋은 사용자가 **명시적으로 요청할 때만** 해요.
- 형식·type·제목 작성법: [CommitMessages.md](CommitMessages.md) ([Conventional Commits](https://www.conventionalcommits.org/))
- 제목·설명 **기본 한글**. scope 목록·언어 override·패치노트는 프로젝트 `AGENTS.md`
- 예: `feat(save): 슬롯 백업 경로 분리`, `docs(common): Unity 기본 보강`
- 요청 없이 `git config` 변경·force push·hard reset 등 파괴적 git 명령을 쓰지 마세요.

## 관련 규칙

- [`.cursor/rules/common/unity-basics.mdc`](../../.cursor/rules/common/unity-basics.mdc)
- 커밋 메시지: [CommitMessages.md](CommitMessages.md) · [`.cursor/rules/common/commit-messages.mdc`](../../.cursor/rules/common/commit-messages.mdc)
- Shell 삭제: [ShellSafety.md](ShellSafety.md)
