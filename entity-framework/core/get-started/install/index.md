---
title: Installing EF Core 
author: divega
ms.author: divega

ms.date: 08/06/2017

ms.assetid: 608cc774-c570-4809-8a3e-cd2c8446b8b2
ms.technology: entity-framework-core

uid: core/get-started/install/index
---
# Installing EF Core

# 安装 EF Core

## Prerequisites

## 先决条件

In order to develop .NET Core 2.0 applications (including ASP.NET Core 2.0 applications that target .NET Core) you will need to download and install a version of the [.NET Core 2.0 SDK](https://www.microsoft.com/net/download/core) that is appropriate to your platform. **This is true even if you have installed Visual Studio 2017 version 15.3.**

为了开发 .NET Core 2.0 应用程序（包括以 .NET Core 为目标的 ASP.NET Core 2.0 应用程序），您需要下载并安装适合您的平台的 .NET Core 2.0 SDK 版本。**即使您安装了 Visual Studio 2017 15.3 版本，情况也是如此。**


In order to use EF Core 2.0 or any other .NET Standard 2.0 library with a .NET platforms besides .NET Core 2.0 (e.g. with .NET Framework 4.6.1 or greater) you will need a version of NuGet that is aware of the .NET Standard 2.0 and its compatible frameworks. Here are a few ways you can obtain this:

为了使用 EF Core 2.0 或任何其他 .NET Standard 2.0 库以及 .NET Core 2.0 以外的.NET平台（例如 .NET Framework 4.6.1 或更高版本），您将需要一个高版本的 NuGet。这里有几个方法可以获得它：

* Install Visual Studio 2017 version 15.3
* If you are using Visual Studio 2015, [download and upgrade NuGet client to version 3.6.0](https://www.nuget.org/downloads)

Projects created with previous versions of Visual Studio and targeting .NET Framework may need additional modifications in order to be compatible with .NET Standard 2.0 libraries:

使用以前版本的 Visual Studio 创建并以 .NET Framework 为目标的项目可能需要进行一些修改才能与 .NET Standard 2.0 库兼容：

* Edit the project file and make sure the following entry appears in the initial property group:
* 编辑项目文件，并确保在初始属性组中出现以下条目：
  ``` xml
  <AutoGenerateBindingRedirects>true</AutoGenerateBindingRedirects>
  ```

* For test projects, also make sure the following entry is present:
* 对于测试项目，还要确保以下条目存在：
  ``` xml
  <GenerateBindingRedirectsOutputType>true</GenerateBindingRedirectsOutputType>
  ```

## Getting the bits
The recommended way to add EF Core runtime libraries into an application is to install an EF Core database provider from NuGet.

将 EF Core 运行时库添加到应用程序的建议方法是从 NuGet 安装。

Besides the runtime libraries, you can install tools which make it easier to perform several EF Core-related tasks in your project at design time, such as creating and applying migrations, and creating a model based on an existing database.

除了运行时库之外，还可以安装 EF Core 工具，以便在设计时执行一些 EF Core 相关的任务，例如创建、迁移以及基于现有数据库创建模型。

> [!TIP]  
> If you need to update an application that is using a third-party database provider, always check for an update of the provider that is compatible with the version of EF Core you want to use. E.g. database providers for previous versions are not compatible with version 2.0 of the EF Core runtime.  
> 如果您需要升级使用第三方数据库提供程序的应用程序，请始终检查与您要使用的 EF Core 版本兼容的提供程序的更新。例如，数据库提供程序的老旧版本就与 EF Core 2.0 不兼容。

> [!TIP]  
> Applications targeting ASP.NET Core 2.0 can use EF Core 2.0 without additional dependencies besides third party database providers. Applications targeting previous versions of ASP.NET Core need to upgrade to ASP.NET Core 2.0 in order to use EF Core 2.0.
> 面向 ASP.NET Core 2.0 的应用程序可以使用 EF Core 2.0，而不需要第三方数据库提供程序之外的其他依赖。以前版本的 ASP.NET Core 应用程序需要升级到 ASP.NET Core 2.0 才能使用 EF Core 2.0。

<a name="cli"></a>
### Cross-platform development using the .NET Core Command Line Interface (CLI)
### 使用 .NET Core 命令行(CLI)进行跨平台开发

To develop applications that target [.NET Core](https://www.microsoft.com/net/download/core) you can choose to use the [`dotnet` CLI commands](https://docs.microsoft.com/dotnet/core/tools/) in combination with your favorite text editor, or an Integrated Development Environment (IDE) such as Visual Studio, Visual Studio for Mac or Visual Studio Code.

要开发面向 [.NET Core](https://www.microsoft.com/net/download/core) 的应用程序，您可以选择将 [`dotnet` CLI 命令](https://docs.microsoft.com/dotnet/core/tools/)与您喜爱的文本编辑器结合使用，也可以使用 Visual Studio、Visual Studio for Mac 或 Visual Studio Code 等集成开发环境（IDE）。

> [!IMPORTANT]  
> Applications that target .NET Core require specific versions of Visual Studio, e.g. .NET Core 1.x development requires Visual Studio 2017, while .NET Core 2.0 development requires Visual Studio 2017 version 15.3.
> 以 .NET Core 为目标的应用程序需要特定版本的 Visual Studio，例如 .NET Core 1.x 开发需要 Visual Studio 2017，而 .NET Core 2.0 开发需要 Visual Studio 2017 15.3 版本。

To install or upgrade the SQL Server provider in a cross-platform .NET Core application, switch to the application's directory and run the following in a command line:

要在跨平台 .NET Core 应用程序中安装或升级 SQL Server 提供程序，请切换到应用程序的目录，然后在命令行中运行以下命令：

``` console
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
```

You can indicate a specific version install in the `dotnet add package` command, using the `-v` modifier. E.g. to install EF Core 2.0 packages, append `-v 2.0.0` to the command.

您可以使用 -v 参数在 `dotnet add package` 命令中指明特定的版本安装。 例如要安装 EF Core 2.0 的版本，请在命令中添加 -v 2.0.0。

EF Core includes a set of [additional commands for the `dotnet` CLI](../../miscellaneous/cli/dotnet.md), starting with `dotnet ef`. In order to use the `dotnet ef` CLI commands, your application’s `.csproj` file needs to contain the following entry:

EF Core 包含一组[ dotnet CLI 的附加命令](../../miscellaneous/cli/dotnet.md)，以 dotnet ef 开头。 为了使用 dotnet ef CLI 命令，您的应用程序的 .csproj 文件需要包含以下条目：

``` xml
<ItemGroup>
  <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="2.0.0" />
</ItemGroup>
```

The .NET Core CLI tools for EF Core also require a separate package called Microsoft.EntityFrameworkCore.Design. You can simply add it to the project using:

EF Core 的 .NET Core CLI 工具也需要一个名为 Microsoft.EntityFrameworkCore.Design 的单独包。 您可以很简单地使用下面命令将它添加到项目：

``` console
dotnet add package Microsoft.EntityFrameworkCore.Design
```

> [!IMPORTANT]  
> Always use versions of the tools packages that match the major version of the runtime packages.
> 始终使用与主要版本的运行时软件包相匹配的工具软件包版本。

<a name="visual-studio"></a>
### Visual Studio development
### Visual Studio 开发

You can develop many different types of applications that target .NET Core, .NET Framework, or other platforms supported by EF Core using Visual Studio.

您可以使用 Visual Studio 开发许多不同类型的应用程序，可以是 .NET Core、.NET Framework 或 EF Core 支持的其他平台。

There are two ways you can install an EF Core database provider in your application from Visual Studio:

有两种方法可以在 Visual Studio 中的应用程序中安装 EF Core 数据库提供程序：

#### Using NuGet's [Package Manager User Interface](https://docs.microsoft.com/nuget/tools/package-manager-ui)

#### 使用 NuGet 的[包管理器用户界面](https://docs.microsoft.com/nuget/tools/package-manager-ui)

* Select on the menu **Project > Manage NuGet Packages**
* 在菜单中选择 **项目 > 管理 NuGet 包**

* Click on the **Browse** or the **Updates** tab
* 点击 **浏览** 或 **升级** 标签

* Select the `Microsoft.EntityFrameworkCore.SqlServer` package and the desired version and confirm
* 选择 `Microsoft.EntityFrameworkCore.SqlServer` 包以及所需版本，点击确认

#### Using NuGet's [Package Manager Console (PMC)](https://docs.microsoft.com/nuget/tools/package-manager-console)

#### 使用 NuGet 的[包管理器控制台 (PMC)](https://docs.microsoft.com/nuget/tools/package-manager-console)

* Select on the menu **Tools > NuGet Package Manager > Package Manager Console**
* 在菜单中选择 **工具 > NuGet 包管理器 > 包管理器控制台**

* Type and run the following command in the PMC:
* 输入并运行一下命令：

  ``` PowerShell  
  Install-Package Microsoft.EntityFrameworkCore.SqlServer
  ```
* You can use the `Update-Package` command instead to update a package that is already installed to a more recent  version
* 你可以使用 `Update-Package` 命令来升级已经安装过的包到最新版本

* To specify a specific version, you can use the `-Version` modifier, e.g. to install EF Core 2.0 packages, append `-Version 2.0.0` to the commands
* 要指定特定版本，可以使用 -Version 参数，例如要安装 EF Core 2.0 软件包，请在命令中添加 -Version 2.0.0

#### Tools
#### 工具

There is also a PowerShell version of the [EF Core commands which run inside the PMC](../../miscellaneous/cli/powershell.md) in Visual Studio, with similar capabilities to the `dotnet ef` commands. In order to use these, install the `Microsoft.EntityFrameworkCore.Tools` package using either the Package Manager UI or the PMC.

Visual Studio 里还有一个 [EF Core 命令的 PowerShell 版本](../../miscellaneous/cli/powershell.md)，具有与 `dotnet ef` 命令类似的功能。为了使用这些，请使用软件包管理器用户界面或 PMC 安装`Microsoft.EntityFrameworkCore.Tools` 软件包。

> [!IMPORTANT]  
> Always use versions of the tools packages that match the major version of the runtime packages.
> 始终使用与主要版本的运行时软件包相匹配的工具软件包版本。

> [!TIP]  
> Although it is possible to use the `dotnet ef` commands from the PMC in Visual Studio, it is far more convenient to use the PowerShell version:
> * They automatically work with the current project selected in the PMC without requiring manually switching directories.  
> * They automatically open files generated by the commands in Visual Studio after the command is completed.

> 尽管可以在 Visual Studio 的 PMC 中使用 dotnet ef 命令，但使用 PowerShell 版本要方便得多：
> * 自动使用 PMC 中选择的当前项目，而无需手动切换目录。
> * 在命令完成后，Visual Studio 会自动打开由命令生成的文件。

> [!IMPORTANT]  
> **Deprecated packages in EF Core 2.0:** If you are upgrading an existing application to EF Core 2.0, some references to older EF Core packages may need to be removed manually. In particular, database provider design-time packages such as `Microsoft.EntityFrameworkCore.SqlServer.Design` are no longer required or supported in EF Core 2.0, but will not be automatically removed when upgrading the other packages.
> **EF Core 2.0中的弃用包**：如果要将现有应用程序升级到 EF Core 2.0，则可能需要手动删除对旧版 EF Core 包的某些引用。特别需要注意， 数据库提供程序设计时包在EF Core 2.0 中不再需要或不再支持，例如 `Microsoft.EntityFrameworkCore.SqlServer.Design` 等，在升级其他包时不会自动删除。