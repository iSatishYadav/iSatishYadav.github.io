---
layout: post
title: "What's New in .NET Libraries for .NET 9"
tags: ["libraries","serialization","json"]
---

[← Previous: What’s New in .NET MAUI for .NET 9](/7-whats-new-in-dotnet-maui-for-dotnet-9)  

.NET 9 adds a wide range of enhancements and new APIs across the base class libraries. These improvements touch everything from low-level data structures and cryptography to JSON serialization, text processing, spans, and advanced math capabilities. The updates enhance performance, security, flexibility, and developer convenience.

## Base64Url Encoding

.NET 9 introduces the new `Base64Url` class, which encodes/decodes data into a Base64 variant safe for URL use. This variant avoids the `+` and `/` characters present in standard Base64, providing a more suitable encoding for query strings and other URL contexts.

```csharp
ReadOnlySpan<byte> data = ...;
string encoded = Base64Url.EncodeToString(data);
```

## Removal of BinaryFormatter

BinaryFormatter is now removed from .NET 9 runtime implementations. Although the APIs still exist, their usage throws exceptions unconditionally. If your application relies on BinaryFormatter, consider migrating to safer and more modern serialization alternatives. For guidance, see the BinaryFormatter migration documentation.

## Collections Improvements

**Span-based Lookups:**  
New capabilities let you look up keys in `Dictionary<TKey,TValue>` and `HashSet<T>` using spans, removing the need to allocate strings. With `Dictionary<TKey,TValue>.GetAlternateLookup<ReadOnlySpan<char>>()`, you can efficiently count words or handle other scenarios with high-performance text processing.

**OrderedDictionary<TKey,TValue>:**  
A new `OrderedDictionary<TKey,TValue>` provides a generic, efficient type for maintaining insertion order while still offering dictionary-level lookups.

**PriorityQueue.Remove():**  
`PriorityQueue<TElement,TPriority>` now includes a `Remove` method that allows emulating priority updates by removing and re-enqueuing items with a new priority, useful in graph algorithms and similar scenarios.

**ReadOnlySet<T>:**  
`ReadOnlySet<T>` provides a read-only wrapper for sets, similar to how `ReadOnlyCollection<T>` and `ReadOnlyDictionary<TKey,TValue>` work for their respective collections.

## Component Model and TypeDescriptor Trimming Support

For trimming scenarios, `TypeDescriptor` introduces new opt-in APIs that register types and fetch properties without triggering trimming warnings. This makes self-contained trimmed applications easier to build without losing type information.

## Cryptography Enhancements

**CryptographicOperations.HashData():**  
A new `HashData` method provides a one-shot hashing API for dynamically chosen algorithms. It streamlines hashing flows and reduces allocations.

**KMAC Algorithm:**  
KMAC (KECCAK-based Message Authentication Code) is now supported, enabling keyed hashing with high-security scenarios. KMAC is available where supported by OpenSSL 3.0 or Windows 11 Build 26016+.

**AES-GCM and ChaChaPoly1305 on iOS/tvOS/MacCatalyst:**  
IsSupported properties for these algorithms now return true on these Apple platforms, expanding cryptographic coverage on mobile and desktop Apple devices.

**X.509 Certificate Loading:**  
A new `X509CertificateLoader` class provides a "one method, one purpose" approach to loading certificates, avoiding content-sniffing and reducing complexity.

**OpenSSL Providers:**  
You can now open keys via OpenSSL providers (like `tpm2`, `pkcs11`), improving hardware security integration scenarios.

**Windows CNG VBS:**  
New flags in `CngKeyCreationOptions` enable using virtualization-based security (VBS) for keys in Windows 11, enhancing key protection against admin-level attacks.

## Date and Time: New TimeSpan.From* Overloads

To avoid floating-point imprecision, new integer-based `TimeSpan` creation methods allow specifying days, hours, minutes, seconds, milliseconds, and microseconds without floating-point inaccuracies.

```csharp
TimeSpan ts = TimeSpan.FromSeconds(seconds: 101, milliseconds: 832); // Precise 00:01:41.832
```

## Dependency Injection Improvements

`ActivatorUtilities.CreateInstance` constructor resolution now correctly prioritizes constructors marked with `[ActivatorUtilitiesConstructorAttribute]`. This ensures that the specified constructor is always chosen.

## Diagnostics and Instrumentation

**Debug.Assert Condition Reporting:**  
If no message is provided, `Debug.Assert` now includes the textual representation of the failed condition, aiding debugging.

**New Activity.AddLink Method:**  
You can now add links to tracing `Activity` objects after creation, aligning .NET’s diagnostic APIs better with OpenTelemetry standards.

**Metrics.Gauge Instrument:**  
A new `Gauge<T>` instrument supports non-additive metric values (like temperature readings or sound levels), following OpenTelemetry specifications.

**Out-of-Proc Meter Wildcard Listening:**  
Meter events can now be listened to via wildcard characters or prefixes, simplifying scenario-specific metric collection with external tools.

## LINQ Extensions

**CountBy and AggregateBy:**  
New LINQ methods `CountBy` and `AggregateBy` streamline operations that previously required `GroupBy`. They allow keyed counting and aggregations without allocating intermediate groupings.

**Index():**  
`Index` enumerates over collections with their indices, simplifying zero-allocation indexing of sequence elements.

## Logging Source Generator

The logging source generator now supports classes with primary constructors, allowing for more concise and efficient logging code in C# 13.

## Miscellaneous Language Features

C# 13 introduces `allows ref struct` constraints. Many core library APIs now support ref struct generic parameters. `SearchValues` expansions improve substring searching and advanced text processing. These enhancements provide more efficient and flexible options for parsers, serializers, and compilers.

## Networking Updates

**SocketsHttpHandler in HttpClientFactory:**  
`HttpClientFactory` now defaults to `SocketsHttpHandler` for better control and performance of connection pooling and rotation.

**System.Net.ServerSentEvents:**  
A new parser simplifies consuming Server-Sent Events (SSE), aiding scenarios like streaming output from AI services or notifications from servers.

**TLS Resume with Client Certificates on Linux:**  
TLS session resumption with client certificates is now supported on Linux, improving security and performance for mutual TLS scenarios.

**WebSocket Keep-Alive and Timeout:**  
WebSocket APIs now support keep-alive pings and connection abortion on non-responses, ensuring more robust WebSocket connections.

## Reflection and Emission

**PersistedAssemblies:**  
`PersistedAssemblyBuilder` enables generating and saving emitted assemblies to disk, bridging gaps in dynamic assembly creation and code generation scenarios.

**TypeName Parsing:**  
The new `TypeName` class offers a parseable, reflection-like representation of type names that doesn’t require runtime environment involvement, simplifying advanced serializer and compiler scenarios.

## Regular Expressions

**[GeneratedRegex] on Properties:**  
Regex source generation now supports partial properties, in addition to partial methods, for compile-time Regex creation.

**Regex.EnumerateSplits:**  
`Regex.EnumerateSplits` provides allocation-free span-based splitting with ranges, a significant performance enhancement over `Regex.Split`.

## System.Text.Json Improvements

**Indentation Options:**  
Fine-grained control over indentation character and size for pretty-printed JSON.

**JsonSerializerOptions.Web:**  
A built-in singleton for ASP.NET Core–style serialization defaults (camelCase, etc.).

**JsonSchemaExporter:**  
Generate JSON schemas for .NET types, aiding OpenAPI and AI integration scenarios.

**Respect Nullable Annotations and Required Constructor Parameters:**  
Options `RespectNullableAnnotations` and `RespectRequiredConstructorParameters` allow strict enforcement of nullability and constructor invariants during serialization.

**Order JsonObject Properties, Custom Enum Names, Multiple JSON Documents, and More:**
- Ordered dictionary–like APIs for `JsonObject`.
- `JsonStringEnumMemberNameAttribute` for custom enum member names.
- Multi-document support in `Utf8JsonReader`.

## Spans and Memory Efficiency

**File Helpers for Spans:**  
Write spans directly to files with `File.WriteAllText(ReadOnlySpan<char>)` and other overloads, avoiding allocations.

**params ReadOnlySpan<T> Overloads:**  
Over 60 new or updated APIs now use `params ReadOnlySpan<T>` for improved performance without array allocations.

**Split Enumeration for Spans:**  
`ReadOnlySpan<char>.Split` now has enumerator APIs for unknown segment counts, removing the need for allocations.

## System.Formats

`TarEntry.DataOffset` now lets you discover the real location of TAR entry data in a stream, supporting advanced large-file scenarios and concurrent reads.

## System.Guid

Guid now supports Version 7 GUID generation, producing time-based, sort-friendly GUIDs. Use `Guid.CreateVersion7()` for such identifiers.

## System.IO and Compression

Transition to zlib-ng for more efficient compression. New compression option types for ZLib and Brotli allow fine-tuned compression level and strategy selection.

## System.Numerics

**BigInteger Limit:**  
A new bit-length limit ensures BigInteger operations remain consistent and well-defined.

**New BigMul APIs, Vector Conversion/Create APIs, and Accelerations:**  
Better numeric APIs, faster vector operations, and more built-in SIMD optimizations.

## Tensors for AI

**Tensor<T>:**  
A new tensor type enabling efficient data manipulation and interoperability with ML frameworks. Build on `TensorPrimitives` and other AI-tailored APIs for zero-copy integrations and higher-dimensional computations.

## Threading

**Task.WhenEach:**  
Process tasks as they complete using `await foreach`.

**Prioritized Channels:**  
`Channel.CreateUnboundedPrioritized` supports elements ordered by priority, not just FIFO.

**Interlocked on More Types:**  
Interlocked now supports byte, sbyte, short, and ushort, and the generic constraints have been relaxed to support primitive and enum types as well.

---

This extensive set of enhancements in the .NET libraries for .NET 9 caters to performance-focused developers, modern security and cryptography needs, next-gen ML and AI workloads, improved JSON and diagnostics, and more. The changes make the base class libraries more consistent, powerful, and ready for complex, data-intensive scenarios.

[Next → What’s New in the SDK and Tooling for .NET 9](/9-whats-new-in-the-sdk-and-tooling-for-dotnet-9)  

**Subscribe to the blog** to stay updated on the latest .NET developments!

**Follow on social media:**

- [Twitter/X: @punskaari](https://twitter.com/punskaari)
- [LinkedIn: @iSatishYadav](https://www.linkedin.com/in/iSatishYadav)