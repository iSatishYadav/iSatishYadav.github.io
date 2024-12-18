---
layout: post
title: "What's New in .NET Aspire 9.0"
tags: ["aspire","observability","cloudnative"]
---

[← Previous: What’s New in the SDK and Tooling for .NET 9](/9-whats-new-in-the-sdk-and-tooling-for-dotnet-9)

[.NET Aspire](https://github.com/dotnet/aspire) is a set of tools, templates, and packages designed to help developers build observable, production-ready apps that embrace cloud-native and distributed computing best practices. .NET Aspire 9.0 marks a significant evolution, introducing support for both .NET 8 (LTS) and .NET 9 (STS), along with community-driven improvements, enhanced tooling, and richer dashboards.

## Key Highlights

- **.NET 8 and .NET 9 Compatibility:**  
  .NET Aspire 9.0 supports both .NET 8 LTS and .NET 9 STS, giving you the flexibility to adopt whichever runtime best suits your organization's support and innovation needs.

- **Community-Driven Enhancements:**  
  Many of .NET Aspire 9.0’s features are guided by community feedback. Join the conversation on [Discord](https://aka.ms/dotnet-discord) or contribute on [GitHub](https://github.com/dotnet/aspire) to help shape the future of .NET Aspire.

## Upgrading and Tooling

**Easier Upgrades to Aspire 9.0:**  
Upgrading to .NET Aspire 9.0 from previous versions is now simpler. The [official upgrade guide](https://learn.microsoft.com/dotnet/aspire/upgrade) provides detailed steps, whether you’re upgrading manually or using the Upgrade Assistant.

**Simplified Tooling Setup:**  
Previously, .NET Aspire depended on installing workloads. In .NET Aspire 9.0, you can install the new SDK directly into your app host project, streamlining environment configuration and setup.

**Templates from NuGet Packages:**  
Templates for creating new .NET Aspire projects have moved to separate NuGet packages. Installing templates now uses `dotnet new install Aspire.ProjectTemplates::9.0.0`, giving you more control over versioning and updates. If you still have the old Aspire workload installed, add `--force` to overwrite existing templates.

## Dashboard and UX Enhancements

**Resource Lifecycle Management:**  
You can now start, stop, and restart individual resources directly from the .NET Aspire dashboard. This granular control helps you debug and manage complex applications without restarting everything. When debugging is attached, it reattaches on restart.

**Mobile-Responsive Dashboard:**  
The Aspire dashboard adapts to various screen sizes, improving accessibility and usability on mobile devices.

**Sensitive Property Masking and Enhanced Logs:**  
Mark properties as sensitive to automatically mask them in the dashboard, preventing accidental exposure of secrets. Colorful console logs now properly render combined ANSI escape codes, providing richer and more informative logs.

## Telemetry and Observability

**Improved Telemetry Filtering and Browser Support:**  
Telemetry filtering now supports attribute-based filters with autocompletion, making it easier to focus on relevant traces. You can also combine telemetry from multiple resource replicas and even send telemetry directly from browser-based SPAs into the Aspire dashboard, providing unified observability across clients and servers.

## App Host and Orchestration

**Waiting for Dependencies and Health Checks:**  
Resources can now wait for dependencies to become ready before starting, leveraging standard .NET health checks. Add HTTP health checks or custom logic to ensure reliable startup sequences. Health check details appear directly in the dashboard.

**Persistent Containers and Resource Commands:**  
Persistent containers continue running outside the app host lifecycle, ideal for scenarios like databases you don’t want to tear down after testing. Also, define custom commands for resources, enabling additional lifecycle or operational tasks accessible via the dashboard’s UI.

**Eventing Model and Container Networking:**  
Hook into global or resource-specific lifecycle events for more customization. All containers now share a default network, simplifying inter-container communication. Converting from Docker Compose becomes more straightforward.

## Integrations and Azure Enhancements

**Redis Insight and OpenAI Support (Preview):**  
Integrate Redis Insight for better database observability and configure OpenAI clients more flexibly, choosing between Azure OpenAI or official OpenAI REST endpoints seamlessly.

**MongoDB Credentials, Improved Azure Resource Naming and Lifecycles:**  
MongoDB integrations now allow specifying credentials. Azure resource customization, previously experimental, is now stable. Adjusting naming policies ensures smoother transitions from .NET Aspire 8 to 9.

**Azure Functions (Preview):**  
One of the most requested features, Azure Functions support, is now in preview. Create and run Azure Functions projects in an Aspire host, debug locally, and deploy to Azure Container Apps seamlessly. Initially supporting common triggers like HTTP, queues, blobs, and service bus, it aligns with .NET Aspire’s goal of simplifying distributed and serverless scenarios.

**Customization of Azure Container Apps:**  
Customize Azure Container App definitions without editing Bicep by using the provided APIs. Scale containers, adjust replicas, and tailor your ACA environment programmatically.

## Conclusion

.NET Aspire 9.0 takes another step toward a streamlined, production-ready developer experience. With support for the latest .NET runtimes, a richer dashboard, robust health checks, flexible telemetry, and broader integration capabilities, Aspire 9.0 helps you build, operate, and manage complex distributed applications with confidence and clarity. Whether you’re leveraging .NET 8 LTS stability or embracing .NET 9 innovations, Aspire 9.0 has you covered.

---

This completes our comprehensive look at what’s new across .NET 9, from runtime and languages to libraries, tooling, MAUI, EF Core, ASP.NET Core, ML.NET, SDK improvements, and finally .NET Aspire 9.0. Together, these advancements illustrate a rapidly maturing, increasingly powerful ecosystem that empowers developers to ship robust, scalable, and innovative solutions.

---
Are you planning to upgrade to .NET 9 or will stay at .NET 8? What features are most exciting to you? Let me know in the comments.


**Subscribe to the blog** to stay updated on the latest .NET developments!

**Follow on social media:**

- [Twitter/X: @punskaari](https://twitter.com/punskaari)
- [LinkedIn: @iSatishYadav](https://www.linkedin.com/in/iSatishYadav)