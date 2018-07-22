# SourceLink

SourceLink is a technology that enables source code debugging of .NET assemblies from NuGet by developers. When creating a NuGet package you use the SourceLink tooling to embed source control metadata inside assemblies and the package, then at debug time tools like Visual Studio can then read that metadata and use it to allow the developer to step into your assemblies source code.

## Using SourceLink

Instructions for using SourceLink can be found on the SourceLink GitHub repository - https://github.com/dotnet/sourcelink/blob/master/README.md

**✓ CONSIDER** using SourceLink to add source control metadata to your assemblies and NuGet package

**✓ CONSIDER** including PDB files in the NuGet package