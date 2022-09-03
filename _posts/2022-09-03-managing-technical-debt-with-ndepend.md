---
layout: post
title: Managing Technical Debt with NDepend!
tags: ["technical debt", "ndepend", ".net"]
---

## What the hell is a Technical Debt?
You are working on a cool new project, want to implement the amazing new design pattern that you learned about few days ago. All is well. Untill, your boss comes to your desk and tells you the release is pre-poned (is that even a word?) by 10 days. WTH man! Now whatever plans you had to make the code readable, testable, SOLID - goes for a toss, and you stuff the code to make up for the early release.

> So you bought some time by writing "not so good code" to meet the deadline.

Let this sink in for a moment.

You know that the code that you had written needs to be refactored, but you don't have the bandwidth (not the internet one) to do so, so you live with this "bad code" - aka `technical debt`.

Well, debts inherently aren't bad, you take debts all the time - Credit Cards, Car Loan, House Loan. But you need to pay the interest, and as long you re-pay, it's well and good. Same goes for the technical debt. It's a trade-off between Product Delivery and impeccable code.

## How do I know that I have a Technical Debt

Some times ago, I did not have any single tool which can give a clear idea what kind of and how much technical debt I have. 

I was looking at different metrics e.g., Code Duplication, Cyclomatic Complexity, Test Coverage, Dependency and Coupling, and more to get an idea.

Then I stumbled upon [`NDepend`](https://www.ndepend.com/?utm_source=blog.satishyadav.com&utm_medium=technical_debt_blog_post).

NDepende can scan your code-base and tell you how much technical debt you have in a single actionable dashboard?


## What is NDepend

NDepend can do much more than that, e.g.,

* Code Rule and Code Query over LINQ (CQLinq)
* Powerful Dependency Graph and Matrix
* Smart Technical Debt Estimation
* Quality Gates
* In-Depth Issues Management
* Trend Monitoring
* Harness Test Coverage Data
* Code Quality and Code Metrics
* Detect Dependency Cycles
* Code Diff since Baseline
* Enforce Immutability and Purity
* Complexity and Diagrams
* Continuous Integration Reporting
* Warnings on Build
* Process Health

and more. 

They consider themselves, _The "Swiss Army Knife" for .NET Developers, Architects and Teams_

Visit their [official site](https://www.ndepend.com/?utm_source=blog.satishyadav.com&utm_medium=technical_debt_blog_post) to know more.

_NDepende team was generous to give me a copy of their license to try out the product_

If you're new to NDepend or want to know how to install and get started, folks at NDepend have written a wonderful step-by-step documentation.

> Thing I like about NDepend is, it gives me a visual dashboard which is actionable. And all the data it provides, it has LINQ queries to support that and accommodate custom rules as well.

## How to find out Technical Debt

For this post, I've taken the [Clean Architecture repo](https://github.com/jasontaylordev/CleanArchitecture?utm_source=blog.satishyadav.com&utm_medium=technical_debt_blog_post) from [Jason Taylor](https://github.com/jasontaylordev?utm_source=blog.satishyadav.com&utm_medium=technical_debt_blog_post). If you don't know Jason, he's the Clean Architecture guy, a great developer, trainer, architect, and more.

Once you clone the repo in Visual Studio, here's how the Project structure looks like:


![project-structure](/images/project-structure.png)

An Angular SPA with Application Layer, Domain Layer, Infrastructure Layer - basically the Clean Architecture.

Attached the NDepend to this solution:
![attach-to-solution](/images/attach-to-solution.png)

NDepend will detect the projects and exclude test projects. Click on Analyze X NET Assemblies.

![pre-run](/images/pre-run.png)

Give it some time to finish.

![finished](/images/finshed.png)

Click on the View NDepend Dashboard.


## Dashboard
The dashboard gives you plethora of information about the Project code quality, lines of code, issues, comments, but we're interested in technical debt.

![dashboard](/images/project-dashboard.png)

In this case, you can see there is a 5.56% of technical debt. Well done, Jason!

> The Smart Technical Debt feature of NDepend also tell us how many days it would take us to resolve the technical debt.

Amazing, right?

Additionally, it gives us the Rating of the project based on Technical Debt. In our case *B*. Pretty good. And how much effort is required to reach to *A*.

## Exploring Technical Debt

If you click on the rating, NDepend will show you the hot-spots of the code where most of the debt is.

![hotspot](/images/hotspot.png)

Clicking on the Debt % gives list of all the issue

![rules](/images/rules.png)

Click on a specific rule to find out the details  and what all code has contributed to this technical debt.

![rule-detail](/images/rule-detail.png)

 In the above example, our code base has violated following rule:

 • Rule Name: Avoid namespaces dependency cycles
 • Rule Id: ND1401
 • Rule Explicit Id: AvoidNamespacesDependencyCycles

 • Rule Description:  

This rule lists all application namespace dependency cycles. Each row shows a different cycle, indexed with one of the namespace entangled in the cycle. 

Read our white books relative to partitioning code, to know more about namespaces dependency cycles, and why avoiding them is a simple yet efficient solution to clean the architecture of a code base. [https://www.ndepend.com/docs/white-books](https://www.ndepend.com/docs/white-books?utm_source=blog.satishyadav.com&utm_medium=technical_debt_blog_post)

• How to Fix Issues of this Rule:  

Removing first pairs of mutually dependent namespaces will eliminate most namespaces dependency cycles. This is why it is recommended to focus first on matches of the default rule Avoid namespaces mutually dependent before attempting to fix issues of the present rule. 

Once all mutually dependent namespaces occurrences are solved, remaining cycles matched by the present rule necessarily involve 3 or more namespaces like in: A is using B is using C is using A. 

To browse a cycle on the dependency graph or the dependency matrix, right click a cycle cell in the result of the present rule and export the matched namespaces to the dependency graph or matrix. This is illustrated here: [https://www.ndepend.com/docs/visual-studio-dependency-graph#Entangled](https://www.ndepend.com/docs/visual-studio-dependency-graph#Entangled?utm_source=blog.satishyadav.com&utm_medium=technical_debt_blog_post)

With such a cycle graph visualized, you can determine which dependencies should be discarded to break the cycle. To do so, you need to identify which namespace should be at low-level and which one should be at high-level. 

In the A is using B is using C is using A cycle example, if A should be at low level then C should be at a higher-level than A. As a consequence C shouldn't use A and this dependency should be removed. To remove a dependency you can refer to patterns described in the HowToFix section of the rule Avoid namespaces mutually dependent. 

Notice that the dependency matrix can also help visualizing and breaking cycles. In the matrix cycles are represented with red squares and black cells. To easily browse dependency cycles, the dependency matrix comes with an option: Display Direct and Indirect Dependencies. See related documentation here: [https://www.ndepend.com/docs/dependency-structure-matrix-dsm#Cycle https://www.ndepend.com/docs/dependency-structure-matrix-dsm#Mutual](https://www.ndepend.com/docs/dependency-structure-matrix-dsm#Cycle https://www.ndepend.com/docs/dependency-structure-matrix-dsm#Mutual?utm_source=blog.satishyadav.com&utm_medium=technical_debt_blog_post)

The estimated Debt, which means the effort to fix such issue, doesn't depend on the cycle length. First because fixing the rule Avoid namespaces mutually dependent will fix most cycle reported here, second because even a long cycle can be broken by removing a single or a few dependencies.

• How to Suppress an Issue of this Rule:  

In source code, tag the concerned code element with this attribute:
[SuppressMessage("NDepend", "ND1401:AvoidNamespacesDependencyCycles", Justification="...")]
This attribute requires the compilation symbol CODE_ANALYSIS to be set on each Visual Studio project relying on it. Without CODE_ANALYSIS symbol defined, the attribute is not compiled and the issues are not suppressed.


Pretty detailed, right?

## Next steps

Now you have a basic understanding of what Technical Debt is and how NDepend can take you into your journey of becoming Technical-Debt-free (if that's a thing).

Visit the NDepend site to learn more.

Here's the repo used in this post, give this a star:

[https://github.com/iSatishYadav/CleanArchitectureCodeBase](https://github.com/iSatishYadav/CleanArchitectureCodeBase)

Originally posted at:

[https://blog.satishyadav.com/2022-09-03-managing-technical-debt-with-ndepend](https://blog.satishyadav.com/2022-09-03-managing-technical-debt-with-ndepend)

Happy Coding!