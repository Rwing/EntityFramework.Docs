---
title: Quick Overview - EF Core
author: rowanmiller
translator: Rwing
translation date: 11/13/2017

ms.author: divega

ms.date: 10/27/2016

ms.assetid: bc2a2676-bc46-493f-bf49-e3cc97994d57
ms.technology: entity-framework-core

uid: core/index
---

# Entity Framework Core Quick Overview

Entity Framework (EF) Core is a lightweight, extensible, and cross-platform version of the popular Entity Framework data access technology.

Entity Framework (EF) Core 是倍受欢迎的数据访问技术 Entity Framework 的轻量级、可扩展的以及跨平台的版本。

EF Core is an object-relational mapper (O/RM) that enables .NET developers to work with a database using .NET objects. It eliminates the need for most of the data-access code that developers usually need to write. EF Core supports many database engines, see [Database Providers](providers/index.md) for details.

EF Core 是一个对象关系映射器(O/RM)，它可以让 .NET 开发者使用 .NET 对象操作数据库。 它消除了开发人员通常需要写大段数据访问代码的需求。EF Core 支持许多数据库引擎，详细信息请查看[数据库提供程序](providers/index.md)

If you like to learn by writing code, we'd recommend one of our [Getting Started](get-started/index.md) guides to get you started with EF Core.

如果你想通过编写代码来学习，推荐我们的[入门指南](get-started/index.md)，以帮助你开始使用EF Core。

## Latest version: EF Core 2.0
## 最新版本: EF Core 2.0

If you are familiar with EF Core and want to jump straight into the details of the new version:

如果您熟悉 EF Core 并想直接跳到新版本的细节：

- **[New features in EF Core 2.0](what-is-new/index.md)**
- **[Upgrading existing applications to EF Core 2.0](miscellaneous/1x-2x-upgrade.md)**
- **[EF Core 2.0中的新功能](what-is-new/index.md)**
- **[将现有应用程序升级到EF Core 2.0](miscellaneous/1x-2x-upgrade.md)**


## Get Entity Framework Core
## 获取 Entity Framework Core

[Install the NuGet package](https://docs.nuget.org/ndocs/quickstart/use-a-package) for the database provider you want to use. E.g. to install the SQL Server provider in cross-platform development using `dotnet` tool in the command line:

你可以在 NuGet 中安装你选择的数据库提供者。例如，若想安装跨平台的 SQL Server 提供程序，可以在命令行中这样使用 `dotnet` 命令：

``` console
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
```

Or in Visual Studio, using the Package Manager Console:

或者在Visual Studio中，使用软件包管理器控制台：

``` PowerShell
Install-Package Microsoft.EntityFrameworkCore.SqlServer
```
See [Database Providers](providers/index.md) for information on available providers and [Installing EF Core](get-started/install/index.md) for more detailed installation steps.

查看[数据库提供程序](providers/index.md)以了解更多信息。查看[安装 EF Core](get-started/install/index.md) 获取更详细的安装步骤

## The Model
## 模型

With EF Core, data access is performed using a model. A model is made up of entity classes and a derived context that represents a session with the database, allowing you to query and save data. See [Creating a Model](modeling/index.md) to learn more.

You can generate a model from an existing database, hand code a model to match your database, or use EF Migrations to create a database from your model (and evolve it as your model changes over time).

使用 EF Core 时，需要利用模型进行数据访问。模型由实体类和一个表示数据库会话的派生上下文组成，允许你查询和保存数据。 请参阅[创建模型](modeling/index.md)以了解更多信息。

你可以从现有的数据库生成模型，需要手动编码模型以匹配数据库，或者使用EF Migrations从模型创建数据库（并随着你模型的改变而改变）。

``` csharp
using Microsoft.EntityFrameworkCore;
using System.Collections.Generic;

namespace Intro
{
    public class BloggingContext : DbContext
    {
        public DbSet<Blog> Blogs { get; set; }
        public DbSet<Post> Posts { get; set; }

        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            optionsBuilder.UseSqlServer(@"Server=(localdb)\mssqllocaldb;Database=MyDatabase;Trusted_Connection=True;");
        }
    }

    public class Blog
    {
        public int BlogId { get; set; }
        public string Url { get; set; }
        public int Rating { get; set; }
        public List<Post> Posts { get; set; }
    }

    public class Post
    {
        public int PostId { get; set; }
        public string Title { get; set; }
        public string Content { get; set; }

        public int BlogId { get; set; }
        public Blog Blog { get; set; }
    }
}
```

## Querying

Instances of your entity classes are retrieved from the database using Language Integrated Query (LINQ). See [Querying Data](querying/index.md) to learn more.

使用语言集成查询(LINQ)从数据库中检索实体类的实例。请参阅[查询数据](querying/index.md)以了解更多信息。

``` csharp
using (var db = new BloggingContext())
{
    var blogs = db.Blogs
        .Where(b => b.Rating > 3)
        .OrderBy(b => b.Url)
        .ToList();
}
```

## Saving Data

Data is created, deleted, and modified in the database using instances of your entity classes. See [Saving Data](saving/index.md) to learn more.

使用实体类的实例在数据库中创建，删除和修改数据。请参阅[保存数据](saving/index.md)了解更多信息。

``` csharp
using (var db = new BloggingContext())
{
    var blog = new Blog { Url = "http://sample.com" };
    db.Blogs.Add(blog);
    db.SaveChanges();
}
```
