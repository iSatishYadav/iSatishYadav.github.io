---
layout: post
title: "What's New in EF Core 9"
tags: ["efcore9","data","orm"]
---

[← Previous: What’s New in C# 13](3-whats-new-in-csharp-13.md)  
Entity Framework Core 9 (EF9) continues to evolve as the go-to data access technology for .NET, delivering improvements in querying, modeling, migrations, cloud-native integrations, and performance. Building on EF Core 8, EF9 targets .NET 8 but can also be used with .NET 9, giving you flexibility in which runtime you adopt.

EF9 introduces significant enhancements for working with Azure Cosmos DB, LINQ translations, hierarchical partition keys, and AOT compilation scenarios. It also brings refinements to migrations, model building, and tooling, ensuring a smoother experience for modern data-driven applications.

### Release and Availability

EF9 is scheduled for release in November 2024. Until then, you can use EF9 through daily builds, which contain the latest features and API tweaks. We strongly recommend testing new features against these daily builds to ensure you’re working with the most up-to-date functionality. EF9 supports both .NET 8 (LTS) and .NET 9 (STS), so you can choose the runtime that best fits your needs.

### Major Highlights

**1. Azure Cosmos DB for NoSQL**  
EF9 brings a comprehensive overhaul of the Azure Cosmos DB provider, including:

- **Efficient Partition-Key-Aware Queries:** EF9 automatically detects partition key predicates in LINQ queries, using them to route queries only to the relevant partition. This reduces request units (RUs) and improves performance.
- **Point Reads with Partition Keys and IDs:** If both partition key and ID are specified, EF can perform a direct, cost-effective point read rather than issuing a full SQL query.
- **Hierarchical Partition Keys:** EF9 fully supports hierarchical partition keys, allowing you to take advantage of Azure Cosmos DB’s multi-level partitioning for finer-grained data partitioning and performance optimization.
- **Expanded LINQ Support:** The provider now translates more LINQ operations, supports querying over primitive and non-primitive collections, and offers improved function translations (e.g., `string.Contains`, date/time components).
- **JSON Alignment and Simpler IDs:** EF9 uses a more natural JSON mapping, removing discriminators from `id` fields and changing default discriminator names to `$type`. This improves interoperability with external systems and better aligns with JSON standards.
- **Vector Similarity Search (Preview):** Azure Cosmos DB vector search can be integrated with EF9, allowing vector-based semantic searches natively.
- **Pagination and Continuation Tokens:** Paginate through results efficiently using continuation tokens, rather than relying on costly `Skip/Take` operations.
- **Safer Raw SQL Queries:** Use `FromSql` (rather than `FromSqlRaw`) for parameterized and safe raw SQL operations.

**2. LINQ and Query Translation Improvements**  
EF9 continues to refine its LINQ provider, improving SQL translation and performance:

- **Pre-Compiled Queries and AOT:** EF9 introduces experimental support for NativeAOT and pre-compiled queries. LINQ queries can be pre-compiled into interceptors containing SQL and materialization logic, significantly improving startup performance.
- **Table and Projection Pruning:** EF9 removes unnecessary JOINs and projections, generating cleaner and potentially more performant SQL.
- **GREATEST/LEAST Functions:** New translations leverage SQL Server 2022’s `GREATEST` and `LEAST` functions for simpler and more efficient code.
- **Parameterization Control:** Control parameterization using `EF.Parameter` and `EF.Constant` to force or prevent parameterization, balancing query plan reuse against potential performance gains.
- **Inlined Subqueries and Aggregates:** Complex queries involving aggregates and subqueries are now translated more naturally, often requiring fewer database round trips.
- **Consistent Null and Comparison Semantics:** EF9 ensures consistent behavior with nullable comparisons, matching C# semantics and aligning results across different providers.

**3. Enhanced Modeling and Compilation**  
Model building sees new features to reduce startup time and simplify configuration:

- **Auto-Compiled Models:** EF9 can automatically discover and use compiled models without requiring manual `UseModel` calls. With MSBuild integration, compiled models are automatically regenerated as the model changes, reducing friction.
- **Read-Only Primitive Collections:** Beyond arrays and mutable lists, EF9 supports read-only collections and lists of primitive types. This provides more flexibility in designing read-only domain models.
- **SQL Server Fill-Factor Support:** Configure `fill-factor` for keys and indexes on SQL Server, controlling how index pages are filled and improving index maintenance and performance.
- **More Extensible Conventions:** EF9 makes it easier to build custom conventions or extend existing ones, improving control over how models are constructed.

**4. Migrations and Seeding**  
Migrations and database initialization also benefit from enhancements:

- **Concurrent Migration Protection:** EF9 introduces locking to prevent multiple migrations from running concurrently, protecting your database from corruption.
- **Warnings for Non-Transactional Operations:** EF9 warns if a migration contains non-transactional operations alongside transactional ones, encouraging safer migration patterns.
- **Improved Data Seeding APIs:** Use `.UseSeeding` and `.UseAsyncSeeding` to conveniently insert initial data during context initialization.
  
**5. Tooling Improvements**  
The `dotnet ef` command experiences fewer unnecessary rebuilds, improving developer productivity. The team welcomes feedback to ensure these improvements don’t have unintended consequences.

### Other Notable Updates

- **HierarchyId Improvements:** EF9 introduces sugar methods to easily generate child HierarchyId nodes, making hierarchical data handling more intuitive.
- **More Efficient Negation and Conditional Translations:** EF9 refines the SQL it generates around logical negations, CASE statements, and conditions, often leading to shorter, more direct SQL.
- **Better Azure SQL and Azure Synapse Support:** EF9 can now target Azure SQL or Azure Synapse specifically, enabling better SQL generation tailored to these environments.

### Conclusion

EF Core 9 represents a substantial leap forward in cloud readiness, performance optimization, AOT integration, and interoperability with JSON-based and vector-based workloads. Whether you’re building with Azure Cosmos DB or optimizing SQL queries on relational databases, EF9 delivers greater control, safer migrations, and improved startup times.

In the next installment, we’ll explore **What’s New in ASP.NET Core 9.0**, examining how the latest changes improve web development, scaling, and performance on the modern web platform.

[Next → What’s new in ASP.NET Core 9.0](5-whats-new-in-aspnet-core-9-0.md)

**Subscribe to the blog** to stay updated on the latest .NET developments!

**Follow on social media:**

- [Twitter/X: @punskaari](https://twitter.com/punskaari)
- [LinkedIn: @iSatishYadav](https://www.linkedin.com/in/iSatishYadav)