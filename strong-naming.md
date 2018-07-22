# Strong Naming

## What is strong naming

Strong-naming is a contraversional subject in the .NET community. There are definite benefits and definite costs to strong-naming, and there is constant debate over whether open source libraries should be strong-named.

When an assembly is strong-named with a private certificate it creates a unique identity and help prevent assembly conflicts. The downside to strong-naming is strict loading of assemblies by the old .NET Framework on Windows kicks in once an assembly is strong named. A strong-named assembly reference must exactly match the version referenced by an assembly, forcing developers to configure binding redirects when using the assembly. When .NET developers complain about strong-naming what they are actually complaining about is stict assembly loading. Fortunatly .NET Core relaxes this restriction and removes the main downside of strong-naming.

Strong-naming is also viral. A strong-named assembly can only reference other strong-named assemblies. If you choose not to strong-name an assembly then anyone who needs strong-naming can not use your library.

**✓ CONSIDER** strong-naming your project assemblies. Strong-naming allows assemblies to be:

  1. Referenced by other strong-named assemblies
  2. Stored and referenced in the Global Assembly Cache (GAC)
  3. Used by applications with plug-in architectures that require strong-named assemblies

**✓ CONSIDER** checking in the private key associated with an assembly into your source control system. This makes it possible for other developers to recompile the library with the same identity.

**✓ CONSIDER** incrementing AssemblyVersion on only major version changes to help users reduce binding redirects.

**X DO NOT** publish strong-named and non-strong-named versions of your project, e.g. Contoso.Api and Contoso.Api.StrongNamed. If an application ends up depending on both packages they will end up with type name conflicts.