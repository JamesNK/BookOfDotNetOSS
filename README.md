# The Book of .NET OSS

The Book of .NET OSS is a living resource to help answer common technical questions from .NET open source project owners and maintaners.

The goal of this website is to bring together the collective wisdom and best practices of open source project owners in one central place instead of being spread across GitHub, StackOverflow and Twitter discussions. We want to help the .NET community to produce high quality, stable .NET libraries for all developers.

## Table of Contents

* [Getting started](./getting-started.md) **TODO**
* [Cross-platform targeting](./cross-platform-targeting.md) **TODO**
* [NuGet](./nuget.md)
  * [SourceLink](./sourcelink.md)
* [Versioning](./versioning.md)
  * [Breaking changes](./breaking-changes.md)
* [Signing](./signing.md) **TODO**
  * [Strong naming](./strong-naming.md)

## Recommendations

The Book of .NET OSS provides a brief description of each topic to introduce why it is important, and then gives a list of recommendations for your OSS project using **Do**, **Consider**, **Avoid** and **Do not**. The wording of each recommendation indicates how strongly it should be followed. For example a **Do** recommendation is one that should almost always be followed:

**✓ DO** choose an [OSS license](https://choosealicense.com/).

On the other hand **Consider** recommendations should generally be followed, but there are legitimate exceptions to the rule and you should not feel bad about not following the guidance:

**✓ CONSIDER** using SemVer to version your NuGet package

**Do not** indicates something you should almost never do:

**X DO NOT** publish strong-named and non-strong-named versions of your project, e.g. `Contoso.Api` and `Contoso.Api.StrongNamed`.

And finally less strong, **avoid** recommendations are something this is not a good idea, but breaking the rule sometimes makes sense:

**X AVOID** grib

## How Can I Help?

1. Please contribute your knowledge to the documentation.
2. Let developers know the documentation exists when a question comes up.

## License

The Book of .NET OSS is licensed under the [Creative Commons Attribution 4.0 International Public License](https://creativecommons.org/licenses/by/4.0/).