# Getting Started

Some first steps to creating and publishing a .NET OSS project:

1. Download the tools useful for developing a .NET library:

    * [.NET Core SDK](https://www.microsoft.com/net/download) contains everything you need to compile a .NET library and NuGet package.

    * [Visual Studio Community](https://visualstudio.microsoft.com/downloads/) is a fully featured IDE for Windows that is free for OSS projects. [Visual Studio Code](https://code.visualstudio.com/Download) is a free cross-platform IDE.

    * [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer#readme) lets you view NuGet package metadata and content.

2. Create a [GitHub](https://github.com/) repository and choose an [OSS license](https://choosealicense.com/).

3. Plan early for your library to be [cross-platform](./cross-platform-targeting.md). .NET runs in many places, the more people you can reach the better.

4. Manage what [dependencies](./dependencies.md) your library will reference. There is a big eco-system of packages to use but dependencies are a common source of friction.

5. Decide on [strong naming](./strong-naming.md) your library.

6. [Create a NuGet package](./nuget.md) (with [SourceLink enabled](./sourcelink.md)) and publish to nuget.org.

7. [Iterate and version](./versioning.md), minimizing [breaking changes](./breaking-changes.md). Every developer who uses your library makes an investment in it. Get them new features without breaking what they already have.

**✓ DO** choose an [OSS license](https://choosealicense.com/). A project without a license defaults to exclusive copyright.

**✓ DO** host your project on [GitHub](https://github.com/) or another online distributed source control service.

---

[Home](./README.md)