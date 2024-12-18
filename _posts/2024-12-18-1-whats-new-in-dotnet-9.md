---
layout: post
title: "What's New in .NET 9"
tags: ["dotnet9","framework","release"]
excerpt_separator: <!--more-->
---

.NET 9 introduces a set of features and improvements designed to support modern application development. This release builds on the capabilities introduced in .NET 8, placing a stronger emphasis on cloud-native scenarios, performance optimizations, and improved developer productivity. As a standard-term support (STS) release, .NET 9 receives 18 months of support, giving organizations sufficient time to adopt and integrate it into their workflows.
<!--more-->
## Emphasis on Cloud-Native and Containerized Workloads

Cloud-native architectures and container-based deployments are standard practice for modern applications. .NET 9 aligns with these trends by refining the framework’s capabilities for distributed, scalable systems. This includes adjustments to runtime behavior, library enhancements that streamline serialization and network I/O, and improved integration points for AI and machine learning workloads—all of which are increasingly relevant in orchestrated, cloud-hosted environments.

For example:

- **Runtime Adjustments for Cloud Scale:** Changes in garbage collection and performance heuristics are designed to better handle highly variable workloads common in cloud scenarios. Dynamic memory management improvements help applications adapt to fluctuating demand without manual intervention.

- **Optimized Communication and Serialization:** Enhancements in **System.Text.Json**, such as support for nullable reference type annotations, exporting JSON schemas from types, and new options for customizing JSON indentation, reduce overhead in microservices that frequently communicate using JSON-based payloads.

## Performance Improvements from Top to Bottom

Performance has been a central priority across multiple layers of .NET 9:

- **Runtime-Level Optimizations:** Enhanced code generation, loop optimizations, inlining strategies, and Arm64 vectorization result in more efficient execution paths. The runtime also introduces a new attribute model for feature switches, enabling libraries to toggle functionality at compile or link time, which can shrink binary size and improve startup times.

- **Library Improvements:** Beyond serialization, improvements to LINQ (like the new `CountBy` and `AggregateBy` methods), priority queues (new `Remove` method for easier priority updates), cryptographic operations (a new `CryptographicOperations.HashData` and KMAC algorithms), and reflection APIs help developers write faster and more efficient code with fewer allocations and better resource usage.

- **Refined Tooling and SDK Features:** A more flexible SDK, improved NuGet security audits (now including transitive references by default), and a default-enabled terminal logger enhance the reliability and traceability of builds. The terminal logger provides more concise and usable summaries, making it easier to identify performance regressions or issues in complex projects. Additionally, new MSBuild script analyzers ("build checks") are available to help identify and fix common build-related issues.

## AI and Machine Learning Support

As applications increasingly integrate AI-driven features, .NET 9 introduces building blocks that simplify the adoption of machine learning and language model capabilities:

- **Microsoft.Extensions.AI and Microsoft.Extensions.VectorData:** These packages provide a unified layer of abstractions to interact with AI services, embeddings, vector stores, and middleware. This uniform API surface reduces the complexity of integrating AI features, eliminating the need for custom glue code.

- **TensorPrimitives and Tensor<T>:** New tensor APIs enable efficient manipulation of multi-dimensional data, crucial for tasks like model inference, image processing, or advanced analytics. These APIs are SIMD-optimized and designed to interoperate efficiently with AI frameworks like ML.NET, TorchSharp, and ONNX Runtime. TensorPrimitives now supports nearly 200 operations (up from 40), generic overloads for different numeric types, and improved performance through SIMD optimizations.

## Language Updates and Enhanced Developer Experience

.NET 9 ships with updates to C# (version 13) and F# (version 9), providing language-level features that simplify coding patterns and modernize idioms:

- **C# 13:** Introduces `params` collections, a new lock type and semantics, a new `\e` escape sequence, method group natural type improvements, implicit indexer access in object initializers, ref locals in async and iterator methods, and `allows ref struct` constraints for generics, along with partial properties and indexers.

- **F# 9:** Adds nullable reference types, discriminated union `.Is*` properties, partial active patterns returning bool, improved tooling support, and other performance and productivity enhancements.

These language updates help developers write safer, more maintainable code and take advantage of modern constructs that improve both productivity and safety.

## Broad Ecosystem Enhancements

ASP.NET Core 9.0 gains optimizations like handling static files more efficiently at build and publish time, Blazor enhancements (hybrid and web app templates, reconnection improvements), API OpenAPI generation, enhanced native AOT support, and security improvements. ML.NET 4.0 brings improved configuration options, ONNX model loading from streams, tokenizer capabilities, and TorchSharp integration for new model families. .NET MAUI focuses on performance, reliability, Native AOT and trimming enhancements, a new TitleBar control on Windows, and a HybridWebView.

EF Core 9 refines Azure Cosmos DB support, steps towards AOT compilation, and pre-compiled queries, while the libraries add LINQ improvements, JSON schema generation, and reflect new methods like `CountBy` and `AggregateBy`.

Windows Presentation Foundation (WPF) and Windows Forms also see enhancements, with modern theming, improved ligature support in fonts, no more `BinaryFormatter`, and rendering improvements for code generation and debugging scenarios.

## Engaging with the Community and Looking Ahead

The .NET team actively posts .NET 9 preview updates and discussions on GitHub, allowing developers to stay informed, ask questions, and provide direct feedback. This open dialogue helps refine features before general availability.

**To Learn More:**  
- [Download .NET 9](https://aka.ms/dotnet-download) to begin experimenting with the latest improvements.  
- Explore the official documentation for detailed guidance on new APIs, runtime settings, and advanced scenarios.  
- Check out .NET 9 GitHub Discussions for ongoing previews, Q&A, and community feedback.

[Next → What’s New in the .NET 9 Runtime](/2-whats-new-in-dotnet-9-runtime)  

**Subscribe to the blog** to stay updated on the latest .NET developments!

**Follow on social media:**

- [Twitter/X: @punskaari](https://twitter.com/punskaari)
- [LinkedIn: @iSatishYadav](https://www.linkedin.com/in/iSatishYadav)