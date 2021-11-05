---
layout: post
title: 🆕 SQL Server 2022 First Look - Top 5 New Features (Bonus 5 Features)
tags: ["SQL Server", "SQL Server 2022", "SQL"]
---

Microsoft [announced](https://cloudblogs.microsoft.com/sqlserver/2021/11/02/announcing-sql-server-2022-preview-azure-enabled-with-continued-performance-and-security-innovation/) the first private preview of SQL Server 2022 claiming "the most Azure-enabled release of SQL Server yet, with continued innovation in performance, security, and availability".

In this post we're going to have a look on top 5 most interesting features.

## 5. Ledger (Blockchain) Support
SQL Server 2022 introduces new Ledger capabilities for creating Blockchain like immutable records to ensure data integrity. If somebody modifies the record, it would no longer be valid.

It would be beneficial for scenarios such as internal and external audits.

## 4. Peer-to-peer replica conflict resolution
In a multi-write scenario - With SQL Server 2022, last-write rule is being automated. Now, when a conflict is detected, the most recent modification time will be chosen to be persisted on all replicas. This helps keep your multi-write scenarios running smoothly.

Previously this peer-to-peer replica conflict would stall the whole operation until it was addressed.

## 3. Intelligent Query Processing
Next generation of Intelligent Query Processing (IQP) includes solutions to some of the most common problems we face today, without any code changes required including:

`MAXDOP` and `CE` model feedback using the Query store to create a feedback cycle to automatically adapt and resolve problems with common query patterns.

## 2. Parameter Sensitive Query Plan Caching 
SQL Server has a great Query Optimizer, but one of the issue faced by a lot of people is Parameter Sniffing. SQL Server caches the execution plan for a Stored Procedure based on certain parameters (sniffing the parameters). This is usually good but it might not necessarily be efficient with another set of parameters.

SQL Server 2022 introduces Parameter Sensitive Plan Optimization which can cache multiple plans based on parameters - without requiring any code change.


Before revealing my top pick, let's see some honorable Mentions:
* Query Store is now turned on by default.
* Read Replica Support for Query Store - you can now use Query Store for your Read-Only workloads of your AG (Available Group).
* New extensions to the T-SQL language to support data virtualization and backup/restore with S3 compatible storage systems. Furthermore, T-SQL will support new JSON functions and time-series capabilities.
* Azure Synapse Link - Previously, moving data from on-premises databases, like SQL Server, to Synapse required you to use ETL. Azure Synapse Link for SQL Server 2022 provides automatic change feeds that capture the changes within SQL Server and feed those into Azure Synapse Analytics. It provides near real-time analysis and hybrid transactional and analytical processing with minimal impact on operational systems.
* [Azure Purview](https://azure.microsoft.com/en-in/services/purview/) Integration - Azure Purview as a unified data governance and management service. SQL Server 2022 is integrated with Azure Purview for greater data discovery, allowing you to break down data silos. Through this integration you will be able to:
  * Automatically scan your on-premises SQL Server for free to capture metadata.
  * Classify data using built-in and custom classifiers and Microsoft Information Protection sensitivity labels.
  * Set up and control specific access rights to SQL Server.

Now for the last feature:

## 1. Fully Managed Disaster Recovery in the Cloud
Using SQL Server 2022 and the new link feature for Azure SQL Managed Instance, you now get all the benefits of running a PaaS environment applied to disaster recovery—allowing you to spend less time on setup and management even when compared to an IaaS environment. This works by using a built-in Distributed Availability Group (DAG) to replicate data to a previously deployed Azure SQL Managed Instance as a DR replica site. The instance is ready and waiting for whenever you need it—no lengthy configuration or maintenance is required. You can also use this link feature in read scale-out scenarios to offload heavy requests that might otherwise affect database performance. 

![DR](./assets/dr.png)

Did I miss any other cool feature? Let me know.

Happy Coding! 👨‍💻

