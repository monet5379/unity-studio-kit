---
name: unity-build-pipeline
description: >-
  Unity 6 LTS 플레이어 빌드 — Build Settings·씬, Player/Quality, Mono vs IL2CPP,
  managed stripping, BuildPipeline.BuildPlayer, CI/headless. 빌드 설정·자동화,
  스크립팅 백엔드 선택, 용량 축소, Unity build / IL2CPP / code stripping /
  Addressables 언급 시 사용.
---

# Unity Build Pipeline

Unity 6 LTS 플레이어 빌드를 설정·스크립트·자동화해요. 씬 목록, 플랫폼 타깃,
스크립팅 백엔드, stripping, headless/CI를 다뤄요. API는 **Unity 6 (6000.x)** 기준이에요.
타이틀이 pin한 에디터 버전이 있으면 그쪽을 따릅니다.

## 사용할 때

- Build Settings/Profiles, 플랫폼·스크립팅 백엔드(Mono vs IL2CPP) 선택
- managed stripping으로 빌드 크기 줄이기
- `BuildPipeline.BuildPlayer`로 반복 가능한 빌드 스크립트
- CI/headless (`-batchmode -executeMethod`) 연동
- `ProjectSettings/EditorBuildSettings.asset` 또는 CI 빌드 스크립트가 있을 때

## 사용하지 않을 때

- CI **서비스 설정 전체**(YAML·러너·시크릿) — DevOps 쪽. 이 스킬은 Unity 쪽 API·설정만
- 콘솔/플랫폼 인증·NDA 세부
- 스토어 제출·배포 파이프라인 전체 (타이틀/스튜디오 배포 문서가 있으면 그쪽)

## 프로젝트 override (먼저 확인)

워크스페이스에 `AGENTS.md`·Architecture·기존 Editor 빌드 스크립트가 있으면:

- Unity 프로젝트 루트, 씬 경로, Addressables 프로필, 타깃 플랫폼(예: Switch → Win64 proxy)은 **프로젝트가 이깁니다**
- 이 스킬은 **범용 빌드 패턴**만 제공해요. 샘플 씬/`MyGameRuntime` 이름을 도메인 확인 없이 복사하지 마세요

## 핵심 워크플로

1. **빌드할 씬 목록** — File → Build Profiles/Settings → Scene List, 또는 `EditorBuildSettings.scenes`. 목록에 있고 enabled인 씬만 포함. 인덱스 0이 시작 씬.
2. **플랫폼 타깃** — 필요 시 `BuildTarget` / `EditorUserBuildSettings`로 active target 전환.
3. **스크립팅 백엔드** (Player Settings) — **Mono**(빠른 이터레이션, 데스크톱) vs **IL2CPP**(AOT C++; 많은 플랫폼 필수, 성능·역공학 난이도↑). IL2CPP는 해당 플랫폼 C++ 툴체인 필요.
4. **크기·성능** — Managed Stripping Level(Disabled → Minimal → Low → Medium → High). 반사만 쓰는 코드는 `link.xml`로 보호. Quality Settings는 플랫폼별.
5. **스크립트 빌드** — `BuildPipeline.BuildPlayer(BuildPlayerOptions)` 후 **`BuildReport` 확인**. `Succeeded`가 아니면 파이프라인을 실패 처리.
6. **Headless CI** — `-batchmode -quit -executeMethod`, exit code 확인.
7. **검증** — 빌드가 throw 없이 끝났는지보다, **실제 플레이어 실행**까지 확인.

## 패턴

### 1. 결과 검사하는 스크립트 빌드

```csharp
using UnityEditor;
using UnityEditor.Build.Reporting;
using UnityEngine;

public static class BuildScript
{
    [MenuItem("Build/Windows x64")]
    public static void BuildWindows()
    {
        var options = new BuildPlayerOptions
        {
            scenes = new[] { "Assets/Scenes/Main.unity", "Assets/Scenes/Level1.unity" },
            locationPathName = "Builds/Windows/Game.exe",
            target = BuildTarget.StandaloneWindows64,
            options = BuildOptions.None,            // 개발 빌드는 BuildOptions.Development
        };

        BuildReport report = BuildPipeline.BuildPlayer(options);
        BuildSummary summary = report.summary;

        if (summary.result != BuildResult.Succeeded)
            throw new System.Exception($"Build failed: {summary.totalErrors} errors");
        Debug.Log($"Build OK: {summary.totalSize} bytes in {summary.totalTime}");
    }
}
```

### 2. Headless / CI 호출

```bash
# 성공 시 exit 0; -quit로 에디터 종료; 빌드 서버는 -nographics
Unity -batchmode -quit -nographics \
  -projectPath "/path/to/Project" \
  -executeMethod BuildScript.BuildWindows \
  -logFile -
```

### 3. stripping 보호용 `link.xml`

```xml
<!-- Assets/link.xml — 링커가 사용처를 못 보는 타입 보존 (reflection, JSON, 플러그인) -->
<linker>
  <assembly fullname="MyGameRuntime" preserve="all"/>
</linker>
```

## 함정

- **에디터에선 로드되는데 빌드에 씬이 없음** — Build Settings 목록에 없거나 disabled. `SceneManager.LoadScene`은 목록 씬만 봄.
- **새 머신에서 IL2CPP 실패** — 플랫폼 C++ 툴체인(Windows Build Tools, Android NDK 등) 미설치. Mono는 불필요.
- **빌드에서만 `MissingMethodException`/`TypeLoadException`** — managed stripping이 반사 전용 코드를 제거함. stripping 낮추거나 `link.xml` preserve.
- **`BuildPlayer` 반환 = 성공으로 착각** — 반드시 `BuildReport.summary.result` 확인. 에러 있어도 반환될 수 있음.
- **Addressables가 오래됐거나 없음** — `com.unity.addressables`는 **별도** 콘텐츠 빌드(Build → Addressables)와 올바른 load path 프로필이 필요. 플레이어 빌드만으로는 재빌드되지 않음.
- **Development 빌드를 출시** — `BuildOptions.Development`는 프로파일러·디버그용이라 느림. 릴리스는 `BuildOptions.None`.

## 상세 참조

멀티 플랫폼 CI 스크립트(타깃 전환, 버전 스탬프, 인자 파싱, exit code)와 Addressables content build 호출:

→ [references/ci-build-script.md](references/ci-build-script.md)

공식 문서: `ScriptReference/BuildPipeline.BuildPlayer`, Manual의 player settings·managed code stripping.

## 검증

빌드 스크립트·설정 변경 후:

- `BuildReport.summary.result == Succeeded` (또는 CI에서 non-zero exit)
- 시작 씬·필수 씬이 `EditorBuildSettings`에 enabled
- Addressables 사용 시 content build + 프로필 load path
- 가능하면 산출 플레이어를 한 번 실행

## 출처

[gamedev-skills/awesome-gamedev-agent-skills — unity-build-pipeline](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/tree/main/skills/unity/unity-build-pipeline) (Apache-2.0, Copyright © 2026 Abhishek Barali and contributors)에서 각색했어요. Kit 변경·고지: 저장소 [`NOTICE`](../../../NOTICE).
