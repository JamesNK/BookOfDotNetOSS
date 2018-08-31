# Introduction

The Book of .NET OSS provides recommendations for developers to create strong and stable .NET OSS libraries. This documentation focuses on *what* and the *why* when building a .NET library, not *how*. After each topic there are links to more information, usually to detailed documentation and references.

## Recommendations

With each topic there is a list of recommendations for your OSS project using **Do**, **Consider**, **Avoid** and **Do not**. The wording of each recommendation indicates how strongly it should be followed. For example a **Do** recommendation is one that should almost always be followed:

**✔️ DO** choose an [OSS license](https://choosealicense.com/).

On the other hand **Consider** recommendations should generally be followed, but there are legitimate exceptions to the rule and you should not feel bad about not following the guidance:

**✔️️ CONSIDER** using [SemVer 2.0.0](https://semver.org/) to version your NuGet package.

**Do not** indicates something you should almost never do:

**❌ DO NOT** publish strong-named and non-strong-named versions of your project, e.g. `Contoso.Api` and `Contoso.Api.StrongNamed`.

And finally less strong, **avoid** recommendations are something this is not a good idea, but breaking the rule sometimes makes sense:

**❌ AVOID** NuGet package references that demand an exact version.