---
layout: post
title: "What's New in .NET MAUI for .NET 9"
tags: ["maui","ui","crossplatform"]
---

[← Previous: What’s New in ML.NET](/6-whats-new-in-ml-net)

.NET Multi-platform App UI (.NET MAUI) in .NET 9 focuses on improving overall product quality, test coverage, performance, and stability. While previous releases introduced major new capabilities and controls, the emphasis in .NET 9 is on refining the developer experience, ensuring robust cross-platform performance, and preparing the ecosystem for future enhancements.

## Enhanced Quality and Compatibility

Key improvements in .NET MAUI 9 revolve around comprehensive bug fixes, expanded test coverage, and enhanced end-to-end scenario testing. The product quality investments are detailed in the official release notes:

- [.NET MAUI 9](https://github.com/dotnet/maui/releases/tag/v9.0.100)
- [.NET MAUI 9 RC2](https://github.com/dotnet/maui/releases/tag/v9.0.100-rc.2)
- [.NET MAUI 9 RC1](https://github.com/dotnet/maui/releases/tag/v9.0.100-rc.1)
- [.NET MAUI 9 Previews](https://github.com/dotnet/maui/releases)

**Note on Support Policy:**  
Working with external dependencies like Xcode and Android SDK tools influences .NET MAUI’s support policy, which differs from the standard .NET support lifecycles. For more information, see the [.NET MAUI support policy](https://github.com/dotnet/maui/blob/main/docs/README.md#maui-support-policy).

**Minimum Deployment Targets and Tooling Requirements:**  
- **Xcode 16** compatibility is required for building iOS, iPadOS, tvOS, and macOS apps. Xcode 16 requires macOS 14.5 or later.
- **Deployment targets:** iOS 12.2 and Mac Catalyst 15.0 (macOS 12.0) are now minimum targets, while Android and Windows remain unchanged.

**Workload and NuGet Packages:**  
.NET MAUI ships as both a .NET workload and multiple NuGet packages, enabling developers to pin projects to specific versions or try experimental builds seamlessly. New projects automatically include the required NuGet dependencies.

## New Controls

**HybridWebView:**  
The new HybridWebView control allows you to host rich web content (HTML, JS, CSS) within your .NET MAUI app and communicate bidirectionally between JavaScript and C# code. This is ideal for integrating existing React, Vue, or Angular web apps into a cross-platform native shell, leveraging .NET on the back-end.

**TitleBar for Windows:**  
A new TitleBar control lets you create a custom title bar for Windows apps. You can add search bars, icons, and menus directly into the title bar area, improving the UI/UX of your desktop apps. Mac Catalyst support will arrive in a future release.

## Control Enhancements and Behavioral Changes

- **BackButtonBehavior Binding Mode:**  
  In Shell apps, `IsVisible` and `IsEnabled` on `BackButtonBehavior` now default to `OneWay`, making runtime control of the back button easier via data bindings.

- **BlazorWebView Updates:**  
  By default, the BlazorWebView now uses `0.0.0.1` instead of `0.0.0.0` for hosting content. The underlying disposal behavior has also changed to reduce deadlocks, but you can revert to the legacy behavior if needed.

- **iOS Buttons:**  
  Button layout on iOS now more accurately respects spacing, padding, border width, and margins. Images in buttons are sized to the max available space.

- **CollectionView & CarouselView (iOS & Mac Catalyst):**  
  Optional new handlers based on UICollectionView APIs offer improved performance and stability. Opt into these handlers to enhance your list and carousel performance.

- **Soft Keyboard Input:**  
  New keyboard types (Password, Date, and Time) are supported on `Entry` and `Editor` controls, enabling more precise input scenarios.

- **Text Justification:**  
  Text controls now support `Justify` alignment, letting you distribute text evenly across the width of the container.

- **TimePicker Event:**  
  `TimePicker` adds a `TimeSelected` event for handling changes in selected time values.

- **WebView Process Termination Handling:**  
  `WebView` introduces a `ProcessTerminated` event to handle unexpected web process endings and recover gracefully.

## Compiled Bindings and Performance

**Compiled Bindings in Code:**  
.NET MAUI 9 introduces a Func-based approach for defining bindings in code without string paths, improving performance and compile-time validation. Compiled bindings now also support scenarios previously unsupported, like Source-based bindings and multi-bindings.

**XAML Compiled Bindings:**  
XAML compiled bindings have fewer restrictions—bindings that set the `Source` property and multi-bindings are now supported. By default, non-compiled bindings produce build warnings, encouraging you to adopt compiled bindings for better performance and correctness.

**Dependency Injection and Handler Disconnection:**  
In Shell apps, page registration with the DI container is no longer mandatory unless you’re customizing lifetime behavior. Handlers now disconnect from their controls automatically in most scenarios (for example, when navigating back), but you can override this with a disconnect policy if desired.

## Platform-Specific Improvements and Features

**Multi-Window Activation:**  
On Mac Catalyst and Windows, you can activate a specific window using `Application.Current?.ActivateWindow(window)`.

**Native AOT Deployment (iOS and Mac Catalyst):**  
Opt into Native AOT deployment to reduce app size (up to 2.5x smaller), improve startup times (up to 2x faster), and enhance performance. This requires full trim compatibility and no linker warnings.

**Native Embedding:**  
.NET MAUI 9 includes full APIs for native embedding scenarios. You can now easily wrap a .NET MAUI view and present it as a native view on Android, iOS, or Mac Catalyst.

## Project Templates, Trimming, and Deprecated APIs

**New Project Templates:**  
The .NET MAUI App project template now includes a sample todo app that uses Syncfusion Toolkit controls and SQLite if you opt in, as well as a .NET MAUI Blazor Hybrid and Web App project template.

**Full Trimming Support:**  
Full trimming support is now available. Trimming-incompatible features are removed unless you specify trimmer directives or adopt compiled bindings and new approaches for XAML and data binding.

**Deprecated APIs:**  
- `Frame` is obsolete; use `Border` instead.
- `MainPage` property on `Application` is obsolete; set the initial page via `Window.Page`.
- Legacy measure calls and compatibility layout classes are deprecated.
- Certain hybrid features and dynamic serialization are incompatible with full trimming, and you must use feature switches or alternate patterns.

## Upgrading from .NET 8 to .NET 9

To upgrade, update your Target Framework Monikers (TFMs), adopt compiled bindings, remove reliance on deprecated APIs, and consider enabling full trimming and Native AOT where beneficial. Detailed guidance is provided in the official migration instructions.

---

In short, .NET MAUI 9 concentrates on quality, stability, and performance improvements, making it easier than ever to build high-quality, well-performing cross-platform apps. The introduction of `HybridWebView`, `TitleBar`, enhanced bindings, and improved platform integration paves the way for more flexible and efficient MAUI development moving forward.

[Next → What’s New in .NET Libraries for .NET 9](/8-whats-new-in-dotnet-libraries-for-dotnet-9)

**Subscribe to the blog** to stay updated on the latest .NET developments!

**Follow on social media:**

- [Twitter/X: @punskaari](https://twitter.com/punskaari)
- [LinkedIn: @iSatishYadav](https://www.linkedin.com/in/iSatishYadav)