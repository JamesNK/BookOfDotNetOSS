# Cross-platform Targeting

The modern .NET ecosystem supports multiple operating systems and devices. It is important for .NET OSS projects to support as wide a range of developers as possible, whether they are building an ASP.NET website hosted in Azure, or a .NET game in Unity.

## .NET Standard

.NET Standard is the best way to add cross-platform support to a .NET library. .NET Standard is a specification of .NET APIs that are available on all .NET implementations. Targeting a .NET Standard lets you produce a library that is usable by all platforms that support that version of .NET Standard.

![.NET Standard](../images/platforms-netstandard.png ".NET Standard")

Targeting .NET Standard, and successfully compiling your project, does not guarantee the library will run successfully on all platforms:

1. Platform specific APIs will fail on other platforms, e.g. `Microsoft.Win32.Registry` will succeed on Windows and throw `PlatformNotSupportedException` when used on any other OS.
2. APIs can behave differently, e.g. reflection APIs have different performance characteristics when an application uses ahead-of-time compilation on iOS or UWP.

> [!TIP]
> The .NET team [offers a Roslyn analyzer](https://docs.microsoft.com/en-us/dotnet/standard/analyzers/api-analyzer) to help you discover possible issues.

**✔️ DO** start with including a `netstandard2.0` target.

> Most general purpose libraries should not need APIs outside of .NET Standard 2.0. .NET Standard 2.0 is supported by all modern platforms and is the recommended way to support multiple platforms with one target.

**❌ AVOID** including a `netstandard1.x` target.

> A .NET Standard 1.x is distributed as a granular set of NuGet packages, which creates large package dependency graph and results in developers downloading a lot of packages when building. Modern .NET platforms, including .NET Framework 4.6.1, UWP and Xamarin, all support .NET Standard 2.0. You should only target .NET Standard 1.x if you specifically need to target an older platform.
>
> If you do have a .NET Standard 1.x target then also include a 2.0 target. Modern platforms will use the 2.0 target and older platforms will fall back to 1.x.

**❌ DO NOT** include a .NET Standard target if the library relies on a platform specific app model.

> For example, a UWP control toolkit library depends on an app model that is only available on UWP. App model specific APIs will not be available in .NET Standard.

**More Information**

* [.NET Standard](https://docs.microsoft.com/en-us/dotnet/standard/net-standard)
* [.NET API analyzer](https://docs.microsoft.com/en-us/dotnet/standard/analyzers/api-analyzer)

## Multi-targeting

An alternative way to add cross-platform support to a .NET library is multi-targeting. Multi-targeting involves targeting .NET implementations individually and includes multiple assemblies in a NuGet package. This leverages NuGet's ability to have multiple assemblies in a package and select the best one when added to an application.

You can combine multi-targeting with .NET Standard. For example, a `netstandard2.0` target could be the default implementation and you could provide a .NET implementation specific target that uses implementation specific APIs for additional features. NuGet will automatically select the implementation specific target when possible, e.g. a .NET Core application will use the `netcoreapp2.0` assembly over the `netstandard2.0` assembly in a NuGet package.

![NuGet package with multiple assemblies](../images/nuget-package-multiple-assemblies.png "NuGet package with multiple assemblies")

**✔️ CONSIDER** targeting .NET implementations in addition to .NET Standard.

> Targeting .NET implementations allows you to call platform-specific APIs that are outside of .NET Standard.
>
> Do not drop support for .NET Standard when you do this. Instead, throw from the implementation and offer capability APIs. This way, your library can be used anywhere and supports runtime light-up of features.

**❌ DO NOT** use multi-targeting with .NET Standard if your source code is the same for all targets.

> The .NET Standard assembly will automatically be used by NuGet. Targeting individual .NET implementations increases the `*.nupkg` size for no benefit.

**✔️ CONSIDER** adding a target for `net461` when you're offering a `netstandard2.0` target. 

> Using .NET Standard 2.0 from .NET Framework has some issues that were addressed in .NET Framework 4.7.2. You can improve the experience for developers that are still on .NET Framework 4.6.1 - 4.7.1 by offering them a binary that is built for .NET Framework 4.6.1.

**✔️ DO** distribute your library using a NuGet package.

> NuGet will select the best target for developer and shield them having to pick the appropriate implementation.

**✔️ DO** use a project file's `TargetFrameworks` property when multi-targeting.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <!-- This project will output netstandard2.0 and net471 assemblies -->
    <TargetFrameworks>netstandard2.0;net471</TargetFrameworks>
  </PropertyGroup>
</Project>
```

**More Information**

* [.NET target frameworks](https://docs.microsoft.com/en-us/dotnet/standard/frameworks)
* [Multi-Targeting and Porting a .NET Library to .NET Core 2.0](https://weblog.west-wind.com/posts/2017/Jun/22/MultiTargeting-and-Porting-a-NET-Library-to-NET-Core-20)

## Older Targets

.NET supports targeting versions of the .NET Framework that are long out of support, e.g. .NET 2.0, as well as platforms that are no longer commonly used, e.g. Silverlight and Windows Phone. The value of targeting such old platforms can be easily outweighed by the overhead of programming around missing APIs.

**❌ DO NOT** include a Portable Class Library (PCL) target, e.g. `portable-net45+win8+wpa81+wp8`.

> .NET Standard is the modern way to support cross-platform .NET libraries and replaces PCLs.

**❌ DO NOT** include targets for .NET platforms that are no longer supported, e.g. `SL4`, `WP`.
