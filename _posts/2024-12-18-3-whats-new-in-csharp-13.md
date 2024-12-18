---
layout: post
title: "What's New in C# 13"
tags: ["csharp13","language","features"]
---

[← Previous: What’s New in the .NET 9 Runtime](/2-whats-new-in-dotnet-9-runtime)  
C# 13 introduces a collection of language enhancements that streamline code patterns, enable more powerful generics, improve low-level control, and provide smoother integrations with newer runtime features. These improvements are fully supported on .NET 9, so you can experiment with them using the latest .NET 9 SDK and Visual Studio 2022 releases.

## Overview

C# 13 adds multiple new features and relaxes certain restrictions, making it easier to write concise, high-performance, and safe code. Key enhancements include:

- **`params` Collections**: Broader support for `params` with various collection types beyond arrays.
- **New Lock Type and Semantics**: Integration with the new `System.Threading.Lock` type for improved synchronization.
- **New Escape Sequence `\e`**: A simplified escape sequence for the ESC character.
- **Method Group Natural Type Improvements**: Refined logic for determining a method group’s natural type.
- **Implicit Indexer Access in Object Initializers**: Using the `^` operator (from-end indexing) directly in object initializers.
- **`ref` and Unsafe Contexts in Iterators and Async Methods**: More flexible usage of `ref struct` and unsafe contexts in async and iterator methods.
- **`allows ref struct` Anti-Constraint**: Enabling `ref struct` types as generic type parameters.
- **Implementing Interfaces on `ref struct` Types**: Allowing `ref struct` to implement interfaces (with some restrictions).
- **Partial Properties and Indexers**: Extending partial method concepts to properties and indexers.
- **Overload Resolution Priority**: Letting library authors prioritize certain overloads.
- **Preview: `field` Contextual Keyword**: Introducing a preview feature for directly accessing compiler-generated backing fields.

Each of these changes builds on the language’s existing strengths, providing more expressive and efficient patterns while maintaining safety and compatibility.

## `params` Collections

Previously, the `params` modifier was restricted to arrays. With C# 13, `params` can be applied to a broader range of collection types, including `System.Span<T>`, `System.ReadOnlySpan<T>`, and any type that implements `IEnumerable<T>` and has an `Add` method. This flexibility allows developers to choose data structures that better fit their performance or memory requirements.

For example, you can declare a method that accepts a `ReadOnlySpan<T>` via `params`:

```csharp
public void Concat<T>(params ReadOnlySpan<T> items)
{
    for (int i = 0; i < items.Length; i++)
    {
        Console.Write(items[i]);
        Console.Write(" ");
    }
    Console.WriteLine();
}
```

When using interface types like `IEnumerable<T>` as `params` parameters, the compiler automatically synthesizes the storage for supplied arguments, simplifying code while still providing flexibility.

## New Lock Type and Semantics

The .NET 9 runtime introduces a new `System.Threading.Lock` type for thread synchronization, and C# 13 integrates with it seamlessly. When you use the `lock` statement on a `Lock` object, the compiler uses the `Lock.EnterScope()` API and a `ref struct` to implement the lock’s scope, rather than relying on `System.Threading.Monitor`. This leads to more efficient synchronization and aligns lock semantics with the new runtime capabilities—no additional code changes are required aside from using the new type in your `lock` statements.

## New Escape Sequence: `\e`

The escape character `ESC` (U+001B) can now be represented with the `\e` escape sequence. Previously, you had to rely on `\u001b` or `\x1b`, which could introduce ambiguity if followed by hexadecimal digits. This new escape sequence removes that ambiguity and makes code clearer:

```csharp
string message = "\e[31mRed text\e[0m";
```

## Method Group Natural Type Improvements

C# 13 refines how the compiler determines a method group’s natural type. Previously, if the compiler needed a “natural type” for a method group, it considered all candidate methods and their scopes simultaneously, which could lead to convoluted rules and less predictable results.

Now, the compiler prunes non-applicable candidate methods at each scope before moving outward, more closely mirroring standard overload resolution. This change yields more intuitive behavior for complex method group scenarios involving generics and constraints.

## Implicit Indexer Access in Object Initializers

C# 13 allows using from-end indexing (the `^` operator) within object initializers, making it easier to express initialization logic that references elements from the end of a sequence. For example:

```csharp
var countdown = new TimerRemaining()
{
    buffer =
    {
        [^1] = 0,
        [^2] = 1,
        [^3] = 2,
        [^4] = 3,
        [^5] = 4,
        [^6] = 5,
        [^7] = 6,
        [^8] = 7,
        [^9] = 8,
        [^10] = 9
    }
};
```

This feature eliminates the need to reindex arrays or collections from the front, simplifying initialization for patterns like reverse ordering.

## `ref` and Unsafe Contexts in Iterators and Async Methods

Before C# 13, iterators (`yield return`) and async methods were more restrictive about `ref` locals, `ref struct` usage, and unsafe contexts. C# 13 relaxes these rules, enabling scenarios where:

- Async methods can declare `ref local` variables or `ref struct` variables, as long as they don’t cross `await` boundaries.
- Iterator methods can now contain unsafe contexts, as long as all `yield return` or `yield break` statements remain in a safe context.

These changes allow `System.Span<T>` and similar `ref struct` types to be more widely used, improving performance without sacrificing safety.

## `allows ref struct` Anti-Constraint

Generic constraints in C# 13 now include the `allows ref struct` keyword, which permits `ref struct` types as generic type arguments. This capability makes it possible to write generic algorithms that leverage `Span<T>` or `ReadOnlySpan<T>` without resorting to reflection or unsafe code.

For example:

```csharp
public class C<T> where T : allows ref struct
{
    public void M(scoped T p)
    {
        // p is a ref struct type and must follow ref safety rules
    }
}
```

This unlocks new avenues for performance-sensitive code that works with stack-based data structures.

## Implementing Interfaces on `ref struct` Types

C# 13 allows `ref struct` types to implement interfaces. However, a `ref struct` can’t be converted to the interface type at runtime because that would require boxing, violating ref safety. Furthermore, `ref struct` types must implement all methods of the interface, including those with default implementations.

This feature closes a gap in type capabilities, enabling `ref struct` types to adhere to interface contracts without relying on non-`ref struct` wrappers or complex workarounds.

## Partial Properties and Indexers

You can now declare partial properties and indexers, analogous to how partial methods work. One part can declare the signature, while another part provides the implementation. This feature enhances modularity and code organization, especially in large codebases where splitting property or indexer logic across multiple files can improve maintainability.

## Overload Resolution Priority

With `OverloadResolutionPriorityAttribute`, library authors can influence the compiler’s overload resolution to prefer certain overloads over others. This feature helps guide consumers toward newer, more efficient APIs without introducing breaking changes. It should be used judiciously to maintain code clarity.

## Preview Feature: `field` Keyword

C# 13 introduces `field` as a contextual keyword in property accessors, allowing direct access to the compiler-generated backing field without declaring it explicitly. For example:

```csharp
public partial class C
{
    public partial string Name { get; set; }
}

public partial class C
{
    public partial string Name
    {
        get => field;
        set => field = value.Trim();
    }
}
```

This feature is currently in preview, and feedback from developers will guide its final design and adoption.

## Getting Started

You can try out these C# 13 features by installing the [.NET 9 SDK](https://aka.ms/dotnet-download) and using the latest version of Visual Studio 2022. For more details on feature availability, refer to the [C# language versioning documentation](https://learn.microsoft.com/dotnet/csharp/language-reference/configure-language-version).

Breaking changes and additional documentation can be found in the [breaking changes article](https://learn.microsoft.com/dotnet/core/compatibility/) and the Roslyn feature status pages, which track when features are merged and their current preview status.

## Summary

C# 13 brings a wide range of enhancements that improve language flexibility, performance potential, and developer productivity. Whether you’re working with new runtime features, exploring more efficient synchronization primitives, or leveraging `ref struct` types in more scenarios, C# 13 provides tools that streamline these tasks.

In the next installment, we’ll look into **What’s New in EF Core 9**, including updates for Azure Cosmos DB, AOT compilation, and more.

[Next → What’s New in EF Core 9](/4-whats-new-in-ef-core-9)  

**Subscribe to the blog** to stay updated on the latest .NET developments!

**Follow on social media:**

- [Twitter/X: @punskaari](https://twitter.com/punskaari)
- [LinkedIn: @iSatishYadav](https://www.linkedin.com/in/iSatishYadav)