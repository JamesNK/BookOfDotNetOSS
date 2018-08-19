# SourceLink

SourceLink is a technology that enables source code debugging of .NET assemblies from NuGet by developers. When creating a NuGet package you use the SourceLink tooling to embed source control metadata inside assemblies and the package. Developers who download the package and have SourceLink enabled in Visual Studio can step into the source code using the source control metadata to create a great debugging experience.

[![Newtonsoft.Json SourceLink Demo](../images/sourcelink-youtube-thumbnail.png)](https://www.youtube.com/watch?time_continue=61&v=gyRGhCQPkB4)

## Using SourceLink

Instructions for using SourceLink can be found on the [SourceLink GitHub repository](https://github.com/dotnet/sourcelink/blob/master/README.md).

You can use [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) to confirm SourceLink metadata has been successfully embedded in the package:

![SourceLink in NuGet Package Explorer](../images/nuget-package-explorer-sourcelink.png "SourceLink in NuGet Package Explorer")

**✓ CONSIDER** using SourceLink to add source control metadata to your assemblies and NuGet package.

**✓ CONSIDER** including PDB files in the NuGet package.