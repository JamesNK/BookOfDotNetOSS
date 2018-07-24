# Breaking Changes

It is important for an OSS project to find a balance between stability for existing users and innovation for the future. As developers we lend towards refactoring and rethinking code until it is perfect, but breaking your existing users has a negative impact, especially for low-level libraries.

## Project types and breaking changes

How a project is used by the .NET community changes the effect of breaking changes on end user developers.

The projects that cause the most disruption are low and middle-level libraries like serializers, parsers, IoC containers, DB ORMs, and web frameworks. These building block packages are used by not only end user developers to build applications, but also by other OSS projects as NuGet dependencies. For example if you are building an application and are using an OSS client to call a web service, and the HTTP library the client uses is updated with a breaking change, you have no way to directly fix the OSS client because it is code you don't own. You must either find compatible versions of the client and HTTP library, or submit a fix to the OSS client and wait for a new version. The worst case situation is if you want to use two OSS projects that depend on mutually incompatible versions of a third library.

High level libraries like a suite of UI controls can release breaking changes with much least harm. Because the high-level library is likely only directly referenced in the end user application, in the event of breaking changes the developer can choose to not update to the latest version, or can modify their application to work with the breaking change.

**✓ DO** think about how your OSS project is used by the community when considering major breaking changes.

## Types of Breaking Changes

Not all breaking changes are equally impactful. 

### Source Breaking Change

A source breaking change doesn't effect program execution but will cause compilation errors the next time the application is recompiled. Examples of source breaking changes include adding a new overload that can result in ambiguity in method calls that were unambiguous previously, or changing a parameter name that can break anyone calling that method using named parameters.

```cs
public class Task
{
    // Adding a type called Task will conflict with System.Threading.Task at compilation
}
```

Because a source breaking change only effects compiling an application it is the least disruptive. A developer can fix broken source themselves quite easily.

### Behavior Breaking Change

Behavior changes are the most common breaking change: almost any change in behavior could break someone. Even a bug fix can qualify if users relied on the previously broken behavior.

**✓ CONSIDER** leaving new features off by default if they effect existing users, and let developers opt-in to the feature with a setting.

### Binary Breaking Change

Changing the public API of a library so that assemblies compiled against older versions are no longer able to call it is known as a binary breaking change. For example changing a method's signature by adding a new parameter will cause already compiled assemblies that called it to throw a `MissingMethodException`.

As well as breaking code that uses individual methods and types, a binary breaking change can break an **entire assembly**. Renaming an assembly in `AssemblyNameAttribute` will cause all compiled code that calls it to fail. Adding, removing or changing the strong naming key for an assembly will also break any existing compiled code.

**X DO NOT** change an assembly name.

**X DO NOT** add, remove or change the strong naming key.

**✓ CONSIDER** using abstract base classes instead of interfaces.

  Adding anything to an interface will cause existing types that implement it to fail. An abstract base class allows you to add a default virtual implementation.

**✓ CONSIDER** placing the `ObsoleteAttribute` on types and members that you intent to remove with instructions for fixing their code to no longer use the obsolete API.

  Code that calls types and methods with the `ObsoleteAttribute` will generate a build warning with the message supplied to the attribute. The warnings gives people who user the obsolete API surface time to migrate so that when the when the obsolete API is removed most are no longer be using it.

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

---

[Home](./README.md)