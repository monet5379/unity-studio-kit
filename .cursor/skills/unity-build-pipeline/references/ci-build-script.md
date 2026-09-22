# CI / headless 빌드 스크립트 (Unity 6 LTS)

`unity-build-pipeline` 상세: CLI 인자·플랫폼 전환·버전 스탬프·올바른 exit code를 주는
재사용 Editor 빌드 스크립트예요. `BuildPipeline.BuildPlayer`와 에디터 커맨드라인 인자를
기준으로 해요.

Kit에서 수정·한글화했어요. 원본: [awesome-gamedev-agent-skills — ci-build-script.md](https://github.com/gamedev-skills/awesome-gamedev-agent-skills/blob/main/skills/unity/unity-build-pipeline/references/ci-build-script.md) (Apache-2.0).

## 인자 받는 빌드 메서드

```csharp
using System;
using System.Linq;
using UnityEditor;
using UnityEditor.Build.Reporting;
using UnityEngine;

public static class CIBuild
{
    // 호출 예: -executeMethod CIBuild.Run -buildTarget Win64 -out Builds/Game.exe -version 1.2.3
    public static void Run()
    {
        string[] args = Environment.GetCommandLineArgs();

        string targetArg = ArgValue(args, "-buildTarget", "Win64");
        string outPath   = ArgValue(args, "-out", "Builds/Game.exe");
        string version   = ArgValue(args, "-version", PlayerSettings.bundleVersion);
        bool   dev       = args.Contains("-dev");

        BuildTarget target = targetArg switch
        {
            "Win64" => BuildTarget.StandaloneWindows64,
            "Mac"   => BuildTarget.StandaloneOSX,
            "Linux" => BuildTarget.StandaloneLinux64,
            "Android" => BuildTarget.Android,
            _ => throw new ArgumentException($"Unknown -buildTarget {targetArg}")
        };

        // active target을 바꿔 해당 플랫폼 define·에셋이 쓰이게 함
        EditorUserBuildSettings.SwitchActiveBuildTarget(
            BuildPipeline.GetBuildTargetGroup(target), target);

        PlayerSettings.bundleVersion = version;

        var options = new BuildPlayerOptions
        {
            scenes = EnabledScenes(),
            locationPathName = outPath,
            target = target,
            options = dev ? BuildOptions.Development : BuildOptions.None,
        };

        BuildReport report = BuildPipeline.BuildPlayer(options);
        BuildSummary s = report.summary;

        if (s.result == BuildResult.Succeeded)
        {
            Debug.Log($"[CIBuild] OK {version} -> {outPath} ({s.totalSize} bytes)");
            EditorApplication.Exit(0);
        }
        else
        {
            Debug.LogError($"[CIBuild] FAILED: {s.totalErrors} errors, result={s.result}");
            EditorApplication.Exit(1);
        }
    }

    private static string[] EnabledScenes() =>
        EditorBuildSettings.scenes.Where(sc => sc.enabled).Select(sc => sc.path).ToArray();

    private static string ArgValue(string[] args, string key, string fallback)
    {
        int i = Array.IndexOf(args, key);
        return (i >= 0 && i + 1 < args.Length) ? args[i + 1] : fallback;
    }
}
```

## CI에서 호출

```bash
# -quit로 에디터 종료; 메서드 안 EditorApplication.Exit로 exit code를 확실히 맞춤
Unity -batchmode -nographics \
  -projectPath "$CI_PROJECT_DIR" \
  -executeMethod CIBuild.Run \
  -buildTarget Win64 -out "Builds/Win/Game.exe" -version "1.2.$BUILD_NUMBER" \
  -logFile - || exit 1
```

- `-logFile -`로 로그를 stdout에 보내 CI가 수집하게 해요.
- exit code는 메서드 안 `EditorApplication.Exit(code)`가 신뢰할 만해요. `-quit`만 쓰면 로그에 에러가 있어도 0이 나올 수 있어요.
- 클린 러너에서는 빌드 전에 Unity 라이선스 활성화(`-username`/`-password`/`-serial` 또는 라이선스 파일)를 **별 단계**로 두세요.

## Addressables 콘텐츠 빌드 (쓸 때)

```csharp
using UnityEditor.AddressableAssets.Settings;

// 플레이어 빌드 **전에** Addressables 번들을 빌드. 안 하면 런타임 로드가 실패할 수 있음
public static void BuildContent()
{
    AddressableAssetSettings.BuildPlayerContent(out var result);
    if (!string.IsNullOrEmpty(result.Error))
        throw new Exception($"Addressables build failed: {result.Error}");
}
```

## 주의

- `SwitchActiveBuildTarget`은 시간이 걸리고 reimport를 유발해요. 타깃당 한 번만.
- `Environment.GetCommandLineArgs()`에는 Unity 자체 플래그도 포함돼요. 커스텀 키만 매칭하세요.
- 빌드 서버에 플랫폼 모듈(IL2CPP 툴체인, Android SDK/NDK 등)이 없으면 늦게 툴체인 에러로 실패해요.
- 타이틀 `AGENTS.md`에 Unity 루트·프록시 타깃(예: Switch → Win64)이 있으면 샘플 경로·타깃보다 **프로젝트가 이깁니다**.
