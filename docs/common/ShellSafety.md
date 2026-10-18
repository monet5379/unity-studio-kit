# Shell 삭제 안전

personal · game 공통이다. 잘못된 Shell 삭제로 워크스페이스·형제 clone이 지워지지 않게, **허용된 삭제 절차만** 쓰게 한다.

에이전트 요약: [`.cursor/rules/common/shell-destructive-ops.mdc`](../../.cursor/rules/common/shell-destructive-ops.mdc)

## 한 줄

`cmd` 삭제 명령은 쓰지 않는다. 삭제는 PowerShell `Remove-Item -LiteralPath` + 워크스페이스 prefix 검증 + `Test-Path` + (재귀 시) 채팅 확인만이다.

## 금지

`cmd` 삭제는 플래그와 관계없이 호출하지 않는다. 사용자가 요청해도 아래 허용 절차로만 진행한다.

- `cmd /c rmdir` · `rd` · `del` · `erase`
- PowerShell에서 `cmd /c ...`로 삭제를 넘기는 모든 형태 (`Invoke-Expression`, `Invoke-Command`, `& cmd`, `Start-Process cmd`)
- PowerShell에서 cmd로 `\"` 를 수동 이스케이프하는 중첩 인용
- 확인·워크스페이스 검증 없는 `rm -rf` / `Remove-Item -Recurse -Force`
- 워크스페이스 밖, 드라이브 루트(`C:\`), `$Recycle.Bin`, **상위·형제 clone 루트**
- 휴지통 비우기·Recycle Bin 경로 조작

`/s` 만 빠져도 `/q`·다른 플래그·깨진 인용으로 경로가 드라이브 루트 쪽으로 해석될 수 있다. 닫는 따옴표 직전에 `\` 가 오는 cmd 인용(`"...\Something\"`)도 쓰지 않는다. cmd는 `\"` 를 따옴표 이스케이프로 읽는다.

## 허용

1. **절대 경로**만 쓴다. cwd에 의존하는 상대 경로로 재귀 삭제하지 않는다.
2. **PowerShell 네이티브**만 쓴다. cmd를 끼우지 않는다.
3. `-LiteralPath`를 쓴다. 경로 끝의 `\` 는 뺀다. 따옴표는 단일 인용 `'...'` 을 기본으로 한다.
4. 삭제 전 프리플라이트를 한 뒤에만 `Remove-Item` 한다.

`$workspaceRoot`는 추측하지 말고, 현재 Cursor 워크스페이스(저장소 루트) 절대 경로를 쓴다.

```powershell
$workspaceRoot = 'C:\path\to\repo'   # 실제 워크스페이스(저장소) 루트
$target = 'C:\path\to\repo\Assets\SomeFolder'

if ($target -notlike "$workspaceRoot\*" -and $target -ne $workspaceRoot) {
    throw "Target outside workspace: $target"
}
if (-not (Test-Path -LiteralPath $target)) {
    throw "Path does not exist: $target"
}
# 채팅에서 사용자 확인 완료 후에만 실행
Remove-Item -LiteralPath $target -Recurse -Force
```

## 사용자 확인

아래면 실행하지 말고 채팅에서 확인을 받는다. Shell에서 `Read-Host`로 막지 않는다.

- 재귀 삭제(`-Recurse`) 또는 디렉터리 삭제
- 대상이 워크스페이스 루트에 가깝거나, `.git` · `docs` · `.cursor` · 스크립트 트리에 닿을 수 있는 경우
- 한 번에 여러 트리·글로브 삭제
- 경로 해석이 애매한 경우

```text
다음 경로를 삭제하려 한다:

    <해석된 절대 경로 전체>

이 경로가:
- 워크스페이스 하위인가?
- 의도한 폴더/파일인가?
- 백업/복구 수단이 있는가? (원격 Git 등)

계속하려면 채팅에 yes 라고 답한다.
```

사용자가 명확히 승낙하기 전에 `Remove-Item -Recurse`를 실행하지 않는다.

## Unity / Git

- `Assets/`(및 Addressables 등 에셋 트리) 아래 `.meta`는 Shell로 생성·수정·삭제하지 않는다.
- 추적 중인 에셋/폴더 제거는 **`git rm`**(필요 시 `-r`)을 우선 검토한다. 에디터에서 지울 수 있으면 에디터를 우선한다.
- `Library/` · `Temp/` · `Logs/` 는 캐시라서 git 관점에서는 지워도 되는 축이다. 그래도 워크스페이스 하위 절대 경로 + 프리플라이트 + 사용자 확인은 같다. Unity가 잠근 파일은 실패할 수 있다. 실패하면 범위를 넓혀 다시 시도하지 않는다.
- git으로 추적하는 일반 파일은 `git rm` / `git restore`를 Shell `Remove-Item`보다 우선한다.

## 대안

- 추적 파일 복구: `git restore` / `git checkout`
- 모호한 정리 요청: 삭제 대신 `Get-ChildItem` 목록 또는 `Move-Item`만 한다.
- 휴지통을 복구 수단으로 두지 않는다. `Remove-Item` / `rmdir`은 휴지통을 거치지 않는다.
