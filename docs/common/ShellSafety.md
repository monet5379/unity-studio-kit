# Shell 삭제 안전

personal · game 공통이에요. 잘못된 Shell 삭제로 워크스페이스·형제 clone이 지워지지 않게, **허용된 삭제 절차만** 쓰게 해요.

정본 규칙: [`.cursor/rules/common/shell-destructive-ops.mdc`](../../.cursor/rules/common/shell-destructive-ops.mdc)

## 한 줄

`cmd` 삭제 명령은 쓰지 마세요. 삭제는 PowerShell `Remove-Item -LiteralPath` + 워크스페이스 prefix 검증 + `Test-Path` + (재귀 시) 채팅 확인만이에요.

## 금지

- `cmd /c rmdir` · `rd` · `del` · `erase` (플래그 무관)
- PowerShell에서 `cmd /c ...`로 삭제를 넘기는 모든 형태
- 확인·워크스페이스 검증 없는 `rm -rf` / `Remove-Item -Recurse -Force`
- 워크스페이스 밖·드라이브 루트·형제 clone 루트·휴지통 조작

## 허용 요지

1. 절대 경로 + `-LiteralPath` (trailing `\` 금지)
2. 대상이 현재 워크스페이스 하위인지 검사
3. 재귀·디렉터리 삭제는 채팅에서 사용자 확인 후

## Unity

- `Assets/` 아래 `.meta`는 Shell로 다루지 마세요.
- 추적 에셋 제거는 `git rm`을 우선 검토하세요.
