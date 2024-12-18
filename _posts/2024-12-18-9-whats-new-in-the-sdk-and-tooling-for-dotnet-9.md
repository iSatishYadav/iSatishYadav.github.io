---
layout: post
title: "What's New in the SDK and Tooling for .NET 9"
tags: ["sdk","tooling","productivity"]
excerpt_separator: <!--more-->
---

[← Previous: What’s New in .NET Libraries for .NET 9](/8-whats-new-in-dotnet-libraries-for-dotnet-9)

The .NET 9 SDK introduces several new capabilities and improvements to streamline development workflows, enhance build and test experiences, improve NuGet security and performance, and provide greater flexibility in managing .NET workloads and containers. These updates make the overall .NET ecosystem more productive, secure, and maintainable.
<!--more-->
## Unit Testing Improvements

**Run Tests in Parallel:**  
With deeper MSBuild integration, `dotnet test` can now run tests for the same project across different target frameworks in parallel by default. Parallel test execution scales with the number of available processors, boosting test throughput. You can opt out by setting the `TestTfmsInParallel` property to `false`.

**Enhanced Test Output in Terminal Logger:**  
The MSBuild terminal logger now supports test result reporting, offering richer feedback both during test execution (showing currently running tests) and after (improved formatting of test failures). This integrated experience replaces multiple loggers with a single, unified output.

## .NET Tool Roll-Forward

Previously, .NET global or local tools didn’t always run on newer .NET versions unless tool authors opted in. In .NET 9, you can specify `--allow-roll-forward` when installing or running a tool. This option configures the tool to run on a newer major version of .NET if the exact target version isn’t available, providing greater flexibility and future-proofing for early adopters.

## Terminal Logger Enhancements

The terminal logger, introduced in .NET 8, is now the default for build, test, and related commands in .NET 9. Enhancements include:

- **Enabled by Default:** No need to manually enable it; it provides clickable links, color-coded warnings and errors, and more concise, user-friendly output.
- **Summaries for Failures and Warnings:** The logger now shows total warnings and errors at the end of a build, making it easier to track regressions and understand build quality trends.
- **Improved Multi-line Message Rendering:** Long warnings or errors now appear without repeated file/line prefixes, resulting in cleaner and more readable output.

You can still disable it with `--tl:off` or control behavior through environment variables.

## NuGet Security Audits and Performance

**Auditing Transitive Dependencies by Default:**  
Starting with .NET 9, `dotnet restore` audits **all** package references (including transitive) for known vulnerabilities. This enhances supply-chain security by default, catching more issues early.

**Faster Dependency Resolution:**  
The NuGet dependency resolver in the SDK has been overhauled for better performance and scalability, especially beneficial for large repositories. If you encounter issues with the new resolver, you can revert to the legacy mechanism, but the default experience should yield significant performance gains.

## MSBuild Script Analyzers (BuildChecks)

A new feature called BuildChecks helps identify defects and regressions in your build scripts. By passing `/check` to commands like `dotnet build`, you enable checks that can produce diagnostics for known issues. This feature makes build scripts more maintainable and reliable over time.

## Analyzer Mismatch Mitigation

When running mixed SDK and MSBuild versions, Roslyn analyzers can encounter version mismatches. .NET 9 detects torn SDK scenarios and implicitly downloads a support package (`Microsoft.Net.Sdk.Compilers.Toolset`) to ensure consistent analyzer experiences, preventing related build warnings and errors.

## Workload Sets

Workload sets enable you to pin all installed workloads to a single, stable version until you explicitly update. This approach prevents unintentional updates and ensures consistent workload environments. You can choose your mode (`manifests` or `workload-set`) and easily review current mode status and installation history using `dotnet workload config` and `dotnet workload history`.

## Workload History

`dotnet workload history` provides a timeline of workload installation and modifications for a given SDK installation. This feature helps you understand how workloads have evolved over time, making it easier to revert or audit changes.

## Container Support

**Insecure Registries:**  
The SDK can now publish images to insecure registries. By configuring your Docker or Podman environment and setting `DOTNET_CONTAINER_INSECURE_REGISTRIES`, you can push images to non-TLS or self-signed registries for development and testing scenarios.

**Environment Variable Renaming:**  
Environment variables controlling container publishing now start with the `DOTNET_` prefix instead of `SDK_`. Existing names remain supported for now.

## Code Analysis

.NET 9 adds several new code analyzers and fixers to maintain best practices and improve code quality. New rules include guidance on not passing unnecessary length arguments, advising internal over public types in executables, and ensuring proper usage of hashing APIs, HTTP headers, and streams. For example:

- **CA1872:** Prefer `Convert.ToHexString` over `BitConverter.ToString` for encoding bytes to hex.
- **CA2265:** Avoid comparing `Span<T>` to `null` or `default`.
- **CA2022:** Avoid partial reads with `Stream.Read` by checking return values.

These rules help keep code robust, efficient, and aligned with .NET best practices.

In summary, the SDK and tooling improvements in .NET 9 focus on accelerating feedback loops (faster tests, better terminal output), strengthening security (enhanced NuGet auditing), providing more stable build environments (workload sets, build checks), and granting developers flexibility in container scenarios and runtime configurations. These enhancements streamline daily workflows, reduce complexity, and empower developers to maintain high-quality, secure, and performant .NET applications.

[Next → What’s New in .NET Aspire 9.0](/10-whats-new-in-dotnet-aspire-9-0)

**Subscribe to the blog** to stay updated on the latest .NET developments!

**Follow on social media:**

- [Twitter/X: @punskaari](https://twitter.com/punskaari)
- [LinkedIn: @iSatishYadav](https://www.linkedin.com/in/iSatishYadav)