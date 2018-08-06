# Breaking Changes

It is important for an OSS project to find a balance between stability for existing users and innovation for the future. As developers we lend towards refactoring and rethinking code until it is perfect, but breaking your existing users has a negative impact, especially for low-level libraries.

## Project types and breaking changes

How a project is used by the .NET community changes the effect of breaking changes on end user developers.

* **Low and middle-level libraries** like a serializer, HTML parser, DB ORM, or web framework are the most impacted by breaking changes.

  These building block packages are used by both end user developers to build applications, and by other OSS projects as NuGet dependencies. For example if you are building an application and are using an OSS client to call a web service, and the HTTP library the client uses is updated with a breaking change, you have no way to directly fix the OSS client because it is code you don't own. You must either find compatible versions of the client and HTTP library, or submit a fix to the OSS client and wait for a new version. The worst case situation is if you want to use two OSS projects that depend on mutually incompatible versions of a third library.

* **High level libraries** like a suite of UI controls are less sensitive to breaking changes.

  Because a high-level library is likely directly referenced in the end user application, in the event of breaking changes the developer can choose to not update to the latest version, or can modify their application to work with the breaking change.

**✓ DO** what you can to minimise breaking changes when developing a low-level .NET library.

**✓ CONSIDER** publishing a major rewrite of a library as a new NuGet package.

## Types of Breaking Changes

Breaking changes fall into different categories and are not equally impactful.

### Source Breaking Change

A source breaking change doesn't effect program execution but will cause compilation errors the next time the application is recompiled. Examples of source breaking changes include adding a new overload that can result in ambiguity in method calls that were unambiguous previously, or changing a parameter name that can break anyone calling that method using named parameters.

```cs
public class Task
{
    // Adding a type called Task could conflict with System.Threading.Task at compilation
}
```

Because a source breaking change is only harmful when the developer recompiles their application it is the least disruptive. A developer can fix their own broken source code easily.

### Behavior Breaking Change

Behavior changes are the most common breaking change: almost any change in behavior could break someone. Even a bug fix can qualify if users relied on the previously broken behavior.

**✓ CONSIDER** leaving new features off by default if they effect existing users, and let developers opt-in to the feature with a setting.

### Binary Breaking Change

Changing the public API of a library so that assemblies compiled against older versions are no longer able to call it is a binary breaking change. For example changing a method's signature by adding a new parameter will cause already compiled assemblies that called it to throw a `MissingMethodException`.

A binary breaking change can also break an **entire assembly**. Renaming an assembly in `AssemblyNameAttribute`, or adding, removing or changing an assembly's strong naming key changes the assembly identity, and all compiled code that uses it will fail.

**✗ DO NOT** change an assembly name.

**✗ DO NOT** add, remove or change the strong naming key.

**✓ CONSIDER** using abstract base classes instead of interfaces.

> Adding anything to an interface will cause existing types that implement it to fail. An abstract base class allows you to add a default virtual implementation.

**✓ CONSIDER** placing the `ObsoleteAttribute` on types and members that you intent to remove with instructions for fixing their code to no longer use the obsolete API.

> Code that calls types and methods with the `ObsoleteAttribute` will generate a build warning with the message supplied to the attribute. The warnings gives people who user the obsolete API surface time to migrate so that when the when the obsolete API is removed most are no longer be using it.

```cs
public class Document
{
    [Obsolete("LoadDocument(string) is obsolete. Use LoadDocument(Uri) instead.")]
    public static Document LoadDocument(string uri)
    {
        return LoadDocument(new Uri(uri));
    }

    public static Document LoadDocument(Uri uri)
    {
        // Load the document
    }
}
```

**More Information**

* [A definitive guide to API-breaking changes in .NET](https://stackoverflow.com/questions/1456785/a-definitive-guide-to-api-breaking-changes-in-net)
* [CoreFX Breaking Change Rules](https://github.com/dotnet/corefx/blob/master/Documentation/coding-guidelines/breaking-change-rules.md)

---

[Home](./README.md)