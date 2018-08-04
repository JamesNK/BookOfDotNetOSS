# Cross-platform Targeting

The modern .NET ecosystem supports multiple operating systems and devices. It is important for many OSS projects to support as wide a range of developers as possible.

There are two general ways to add cross-platform support to a .NET library:

1. Target platforms individually and include multiple assemblies in a NuGet package, e.g. project `csproj` targets `net46` and `netcoreapp20` and the NuGet package contains two assemblies
2. Target .NET Standard, a specification for .NET APIs available on all .NET implementations. The single .NET Standard assembly supports multiple frameworks.

You can also combine these two approaches. For example a `netstandard20` target could be the default implementation and you could provide a platform specific target with additional features. NuGet will automatically prefer the platform specific target when possible.

**✓ DO** support multiple .NET platforms if possible.

**More Information**

* [NuGet target frameworks](https://docs.microsoft.com/en-us/nuget/reference/target-frameworks)
* [Multi-Targeting and Porting a .NET Library to .NET Core 2.0](https://weblog.west-wind.com/posts/2017/Jun/22/MultiTargeting-and-Porting-a-NET-Library-to-NET-Core-20)

## .NET Standard

The .NET Standard is a specification of .NET APIs that are available on all .NET implementations. Targeting .NET Standard lets you produce a library that can be used by all platforms that support that version of .NET Standard.

![.NET Standard](./images/platforms-netstandard.png ".NET Standard")

Note that targeting .NET Standard, and successfully compiling your project, does not guarantee the library will run successfully on all platforms:

1. Platform specific APIs will fail on other platforms, e.g. `Microsoft.Win32.Registry` will succeed on Windows and throw `PlatformNotSupportedException` when used on any other OS.
2. APIs can behave differently, e.g. reflection APIs have different performance characteristics when an application uses ahead-of-time compilation on iOS or UWP.

**✓ CONSIDER** including a `netstandard20` target. .NET Standard 2.0 is supported by all modern platforms and is the recommended way to support multiple platforms with one target.

**X AVOID** including a `netstandard1x` target. A .NET Standard 1.x target has a large package dependency graph and will download a lot of packages. Prefer .NET Standard 2.0 and above.

**X DO NOT** include a .NET Standard target if the library relies on a platform specific app model, e.g. library is a UWP control toolkit.

**More Information**

* [.NET Standard](https://docs.microsoft.com/en-us/dotnet/standard/net-standard)

## Older Targets

.NET supports targeting versions of the .NET Framework that are long out of support, e.g. .NET 2.0, as well as platforms that are no longer commonly used, e.g. Silverlight and Windows Phone. The value of targeting such old platforms can be easily outweighed by the overhead of programming around missing APIs.

**X DO NOT** include a Portable Class Library (PCL) target, e.g. `portable-net45+win8+wpa81+wp8`. .NET Standard is the modern way to support multiple platforms.

**X DO NOT** include targets for .NET platforms that are no longer supported, e.g. `SL4`, `WP`.

---

[Home](./README.md)