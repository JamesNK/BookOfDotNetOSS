# Getting Started

1. First get the tools useful for developing .NET OSS projects:

    * [.NET Core SDK](https://www.microsoft.com/net/download) contains the tools required to produce a .NET library and NuGet package.

    * [Visual Studio Community](https://visualstudio.microsoft.com/downloads/) is a fully featured IDE for Windows that is free for OSS projects. [Visual Studio Code](https://code.visualstudio.com/Download) is a free cross-platform IDE.

    * [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer#readme) is useful for viewing NuGet package metadata and content.

2. Plan early for what [platforms the library will target](./cross-platform-targeting.md).

3. Choose whether to [strong name](./strong-naming.md) your library.

4. [Create a NuGet package](./nuget.md) (with [SourceLink enabled](./sourcelink.md)) and publish to nuget.org.

5. Iterate and [version](./versioning.md) the library, minimizing [breaking changes](./breaking-changes.md).