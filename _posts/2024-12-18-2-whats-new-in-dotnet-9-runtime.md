---
layout: post
title: "What's New in the .NET 9 Runtime"
tags: ["runtime","jit","gc"]
excerpt_separator: <!--more-->
---

[← Previous: What's New in .NET 9](/1-whats-new-in-dotnet-9)  

The .NET 9 runtime introduces a range of features and optimizations aimed at improving performance, reducing application size, enhancing security, and providing more flexible deployment options. These enhancements target both core runtime components and the JIT compiler, delivering faster execution times, smaller footprints, and safer execution environments.
<!--more-->
## Attribute Model for Feature Switches with Trimming Support

In .NET 9, two new attributes—`FeatureSwitchDefinitionAttribute` and `FeatureGuardAttribute`—help developers define feature switches that integrate with trimming and Native AOT. By using these attributes, you can toggle areas of functionality at build time, removing unused code paths and reducing application size.

- **`FeatureSwitchDefinitionAttribute`**:  
  This attribute treats a feature-switch property as a compile-time constant during trimming. When a feature is disabled in the app’s configuration, related code paths are removed from the final binary. Consider the following code:

  ```csharp
  if (Feature.IsSupported)
      Feature.Implementation();

  public class Feature
  {
      [FeatureSwitchDefinition("Feature.IsSupported")]
      internal static bool IsSupported => AppContext.TryGetSwitch("Feature.IsSupported", out bool isEnabled) ? isEnabled : true;

      internal static void Implementation() { /* ... */ }
  }
  ```

  By setting `<RuntimeHostConfigurationOption Include="Feature.IsSupported" Value="false" Trim="true" />` in the project file, `Feature.IsSupported` is effectively treated as false, and the call to `Feature.Implementation()` is removed after trimming.

- **`FeatureGuardAttribute`**:  
  This attribute identifies a feature-switch property as a guard for code annotated with `RequiresUnreferencedCodeAttribute`, `RequiresAssemblyFilesAttribute`, or `RequiresDynamicCodeAttribute`. For example:

  ```csharp
  if (Feature.IsSupported)
      Feature.Implementation();

  public class Feature
  {
      [FeatureGuard(typeof(RequiresDynamicCodeAttribute))]
      internal static bool IsSupported => RuntimeFeature.IsDynamicCodeSupported;

      [RequiresDynamicCode("Feature requires dynamic code support.")]
      internal static void Implementation() { /* Uses dynamic code */ }
  }
  ```

  When publishing with `<PublishAot>true</PublishAot>`, this setup avoids certain analyzer warnings and removes unreachable code paths.

## UnsafeAccessorAttribute Support for Generic Parameters

`UnsafeAccessorAttribute`—introduced in .NET 8—allows direct, unsafe access to private type members. In .NET 9, it now supports generic parameters for both CoreCLR and Native AOT scenarios. This expansion enables reflection-free access to generic fields and methods, improving advanced scenarios like performance-sensitive libraries and frameworks.

```csharp
using System.Runtime.CompilerServices;

public class Class<T>
{
    private T? _field;
    private void M<U>(T t, U u) { }
}

class Accessors<V>
{
    [UnsafeAccessor(UnsafeAccessorKind.Field, Name = "_field")]
    public extern static ref V GetSetPrivateField(Class<V> c);

    [UnsafeAccessor(UnsafeAccessorKind.Method, Name = "M")]
    public extern static void CallM<W>(Class<V> c, V v, W w);
}
```

With this feature, code that previously relied on reflection to manipulate generics can now use `UnsafeAccessorAttribute` for more efficient and predictable access.

## Garbage Collection Improvements

**Dynamic adaptation to application sizes (DATAS)**, introduced as an opt-in in .NET 8, is now enabled by default. DATAS adjusts memory usage dynamically based on the application’s long-lived data size. This approach helps the GC maintain a heap size proportional to actual memory requirements, improving overall performance and efficiency in real-world workloads.

For more details, see [Dynamic adaptation to application sizes (DATAS)](https://learn.microsoft.com/dotnet/).

## Control-Flow Enforcement Technology (CET)

CET is now enabled by default on Windows, providing hardware-enforced protection against return-oriented programming (ROP) exploits. CET improves application security by enforcing safer control-flow transitions. Although it may introduce a small performance overhead, CET can be disabled if necessary. This marks a significant step in hardening .NET applications against low-level attacks.

## .NET Install Search Behavior

.NET 9 adds configuration options for how apps locate and load the .NET runtime. Developers can now more tightly control the search behavior, which is useful for private runtime installations or ensuring a stable, known environment.

## Performance Improvements Across the Board

The .NET 9 runtime delivers a wide array of performance optimizations. These improvements span JIT compilation, code generation, loop transformations, exception handling, and more. They include:

- **Loop Optimizations:**  
  Enhanced induction-variable widening, post-indexed addressing on Arm64, strength reduction, and loop counter direction optimizations reduce instruction counts and increase throughput. Common looping patterns—such as iterating over arrays—are now executed more efficiently without any source code changes.

- **Inlining Improvements:**  
  Shared generics that require runtime lookups can now be inlined, reducing overhead and enabling further optimizations. Accesses to thread-local statics on multiple platforms are also more easily inlined, cutting down instruction counts and improving runtime performance.

- **PGO Enhancements:**  
  Dynamic profile-guided optimization (PGO), enabled by default since .NET 8, now drives more decisions, including optimizing type checks and casts based on observed runtime behavior. This leads to faster code paths for the common cases your application actually encounters.

- **Arm64 and SIMD Codegen:**  
  Arm64 benefits from vectorization in `.NET libraries`, multi-register load/store instructions, post-indexed addressing, and store-pair instructions. AVX10v1 support and Arm SVE experimental support introduce new hardware acceleration paths, allowing .NET to leverage cutting-edge CPU instruction sets for even greater speed-ups.

- **Faster Exceptions:**  
  The exception handling model now mirrors the NativeAOT runtime’s approach, eliminating Windows SEH and Unix emulation. As a result, handling exceptions is up to 2-4 times faster in micro-benchmarks, significantly improving scenarios where exceptions are part of normal execution (for example, certain parsing or cancellation operations).

- **Code Layout and Reduced Address Exposure:**  
  The JIT compiler now rearranges basic blocks more effectively, using profile data to reduce branching. It also tracks addressed-exposed locals more accurately, avoiding unnecessary constraints that limit optimization opportunities.

- **Object Stack Allocation for Boxes:**  
  Situations where value types need to be boxed (for example, passing them as objects) can now be optimized by stack-allocating the box when it doesn’t escape the current method. In some cases, the compiler can even reason about the values and remove the boxes entirely, generating more efficient code and reducing allocations.

## Summary

The .NET 9 runtime brings substantial changes under the hood to deliver faster, more secure, and more efficient applications. Developers benefit from:

- Greater control over feature sets and trimming, ensuring leaner deployments.
- Improved performance through advanced JIT optimizations, vectorization, and better code generation strategies.
- Enhanced security via CET and refined exception handling for predictable, safe execution.
- New capabilities that enable low-level code manipulation, improved GC behavior, and better CPU-specific optimizations.

In the next part, we’ll explore **What’s new in C# 13**, the language updates accompanying this release, and how they integrate with the runtime to provide a more productive and modern development experience.

[Next → What’s New in C# 13](/3-whats-new-in-csharp-13)

**Subscribe to the blog** to stay updated on the latest .NET developments!

**Follow on social media:**

- [Twitter/X: @punskaari](https://twitter.com/punskaari)
- [LinkedIn: @iSatishYadav](https://www.linkedin.com/in/iSatishYadav)