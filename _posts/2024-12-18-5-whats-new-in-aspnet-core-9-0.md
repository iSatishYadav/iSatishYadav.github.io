---
layout: post
title: "What's New in ASP.NET Core 9.0"
tags: ["aspnetcore","web","http"]
---

[← Previous: What’s New in EF Core 9](/4-whats-new-in-ef-core-9)  

ASP.NET Core 9.0 streamlines delivering static assets, enhances Blazor development workflows, expands built-in OpenAPI capabilities, improves SignalR tracing and AOT support, and refines authentication and authorization features. In addition, the release introduces performance optimizations, improved debugging and metrics, and various quality-of-life improvements for developers.

## Static Asset Delivery Optimization

Delivering static assets efficiently is a key part of building high-performance web applications. ASP.NET Core 9.0 introduces `MapStaticAssets`, a new endpoint convention that can replace `UseStaticFiles` in most scenarios. This feature leverages build-time preprocessing to compress and optimize your site’s static resources, including CSS and JavaScript files. Benefits include:

- **Build-time Compression:**  
  CSS and JS files are compressed (gzip or brotli) at build time, eliminating the need for on-the-fly compression. This saves CPU cycles and reduces bandwidth usage.
  
- **Content-Based ETags:**  
  ETag headers are generated based on the file’s SHA-256 hash, ensuring the browser re-downloads a file only if its content changes.
  
- **Caching and Stale Asset Prevention:**  
  The runtime sets optimal caching headers and uses asset fingerprints to ensure clients get updated content when files change.

`MapStaticAssets` is ideal for assets known at build and publish time. For more dynamic scenarios or assets served from external sources, `UseStaticFiles` remains a good fit. By default, the optimization works automatically, providing out-of-the-box size reductions of up to 80–90% compared to uncompressed files. This improvement benefits mobile and low-bandwidth environments significantly.

## Blazor Enhancements

**.NET MAUI Blazor Hybrid & Web App Solution Template:**  
A new template allows you to create .NET MAUI native and Blazor Web apps that share the same UI layer. This solution template offers:

- A unified, shared Razor Class Library (RCL) for UI components.
- Automatic generation of a Blazor Web App (global interactivity) and a .NET MAUI Blazor Hybrid app.
- Dependency injection demos to show how to handle environment-specific services.

**Detecting Render Modes, Interactivity, and Location:**  
ASP.NET Core 9.0 provides APIs to detect a component’s execution environment, whether it’s interactive, and which render mode it uses. This makes it easier to write components that behave differently depending on their execution context.

**Improved Reconnection for Server-Side Blazor:**  
The reconnection experience for Blazor Server has been refined:

- Immediate reconnection attempts when revisiting a sleeping tab.
- Automatic page refresh if the server has released the circuit.
- An adaptive backoff strategy for retry intervals and modernized reconnection UI.

**Authentication State Serialization:**  
New APIs make it simpler to add authentication to Blazor Web Apps. You can serialize the authentication state on the server and deserialize it in the browser, enabling pre-initialized authentication states without custom code. This integration works seamlessly with global interactivity and the Individual Accounts authentication scheme.

**Static SSR Pages in Globally-Interactive Blazor Apps:**  
You can now opt certain pages out of global interactivity and render them using only server-side static SSR. This approach is useful for pages that rely heavily on the request/response cycle (for example, operations involving cookies) and cannot be interactively updated.

**Constructor Injection in Razor Components:**  
Razor components now support dependency injection via constructors, providing a familiar and streamlined pattern for injecting services into components.

**WebSocket Compression and CSP for Interactive Server Components:**  
By default, Interactive Server components now use WebSocket compression and set a default CSP frame-ancestors policy. You can disable compression or tighten CSP directives further, balancing security and performance.

**Keyboard Composition Events and InputNumber Enhancements:**  
- `KeyboardEventArgs.IsComposing` helps handle international character input scenarios more accurately.
- `InputNumber<TValue>` now supports `type="range"`, enabling range inputs like sliders with integrated form validation and model binding.

**Enhanced Navigation Events:**  
JavaScript callbacks can be triggered before and after “enhanced navigation,” improving how you handle navigation events in Blazor SSR scenarios.

## SignalR Improvements

**Polymorphic Type Support in Hubs:**  
Hub methods can accept base classes, allowing polymorphic binding of derived types. Annotate classes with `[JsonPolymorphic]` and `[JsonDerivedType]` to enable this scenario.

**Tracing with OpenTelemetry:**  
New `ActivitySource` instrumentation for both server and client hubs helps with distributed tracing. You can see how methods and calls link together across the network, making debugging and telemetry much easier.

**Native AOT and Trimming Support:**  
SignalR now supports trimming and native AOT scenarios, reducing application size and startup time while maintaining real-time communication capabilities.

## OpenAPI Integration

ASP.NET Core 9.0 introduces first-class OpenAPI document generation via `Microsoft.AspNetCore.OpenApi`. This new capability:

- Generates OpenAPI documents for controller-based or minimal APIs.
- Integrates with the .NET toolchain to generate documents at build time.
- Supports customization through document, operation, and schema transformers.
- Works seamlessly with trimming and native AOT.

## Authentication and Authorization Updates

**Pushed Authorization Requests (PAR) for OpenID Connect:**  
The `OpenIdConnectHandler` now supports Pushed Authorization Requests, improving security by sending authorization parameters through back channels rather than the browser’s front channel. This feature is enabled by default if the Identity Provider supports PAR and can be disabled if necessary.

**OAuth/OIDC Parameter Customization:**  
A new `AdditionalAuthorizationParameters` option allows adding arbitrary query parameters without writing custom events or handlers.

**HTTP.sys Extended Authentication Flags:**  
Configure Kerberos credential caching and credential capturing via `EnableKerberosCredentialCaching` and `CaptureCredentials` options, optimizing Windows authentication scenarios.

## Miscellaneous Improvements

**HybridCache (Preview):**  
A new HybridCache API merges the best of `IDistributedCache` and `IMemoryCache` with features like stampede protection, customizable serialization, and performance optimizations. It’s intended to simplify caching patterns and minimize duplication of logic.

**Developer Exception Page Enhancements:**  
The developer exception page now includes endpoint metadata, improved text wrapping, and consistent formatting, making debugging easier.

**Dictionary Debugging Improvements:**  
Key-value collections (headers, query strings, cookies, etc.) have improved debugging layouts, making their contents more readable in Visual Studio’s debugger.

**Graceful Shutdown with IIS & ANCM:**  
A built-in delay helps avoid 503 errors during app restarts or recycles on IIS, configurable via `shutdownDelay`.

**Analyzer for Overridden Authorization:**  
A new analyzer warns when `[Authorize]` attributes are effectively overridden by `[AllowAnonymous]` attributes placed farther away, preventing unintentional security lapses.

**Connection Metrics and Named Pipe Endpoints in Kestrel:**  
Kestrel’s improved `kestrel.connection.duration` metric includes error types, helping diagnose connection issues without verbose logging. Named pipe endpoints now support advanced customization options.

**ExceptionHandlerMiddleware Customization:**  
Configure custom status codes returned by `ExceptionHandlerMiddleware` based on the exception type.

**Opt-Out of HTTP Metrics and Other Features:**
- Metrics can be disabled per endpoint or dynamically per request.
- Data protection keys can be deleted after careful consideration.
- Middleware supports keyed DI injection.
- `dotnet dev-certs https --trust` now works on Linux to trust the ASP.NET Core development certificate in browsers and the system.

**Template Updates:**  
The .NET 9 templates now use the latest versions of Bootstrap, jQuery, and jQuery Validation, ensuring you start with modern, secure, and performant front-end dependencies.

[Next → What’s New in ML.NET](/6-whats-new-in-ml-net)

**Subscribe to the blog** to stay updated on the latest .NET developments!

**Follow on social media:**

- [Twitter/X: @punskaari](https://twitter.com/punskaari)
- [LinkedIn: @iSatishYadav](https://www.linkedin.com/in/iSatishYadav)