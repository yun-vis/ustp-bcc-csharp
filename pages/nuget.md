---
# permalink: /about/
layout: single
title: ".Net File Management"
classes: wide
header:
  image: /assets/images/teaser/teaser.png
  caption: "Image credit: [**Yun**](http://yun-vis.net)"
last_modified_at: 2025-03-31
---

# Project Management

# [An Introduction to NuGet](https://learn.microsoft.com/en-us/nuget/what-is-nuget)
An essential tool for any modern development platform is a mechanism through which developers can create, share, and consume useful code. Often such code is bundled into "packages" that contain compiled code (as DLLs) along with other content needed in the projects that consume these packages.

For .NET (including .NET Core), the Microsoft-supported mechanism for sharing code is NuGet, which defines how packages for .NET are created, hosted, and consumed, and provides the tools for each of those roles.

More packges to install? Please visit [https://www.nuget.org/](https://www.nuget.org/)

```bash
// Check installed NuGet version
$ dotnet nuget --version
```

# Installation Examples

## Install [QuickGraph](https://www.nuget.org/packages/QuikGraph)
```bash
// core
$ dotnet add package QuikGraph --version 2.5.0
// file IO
$ dotnet add package QuikGraph.Serialization --version 2.5.0
// visualization
$ dotnet add package QuikGraph.Graphviz --version 2.5.0
```

## Install [SkiaSharp](https://www.nuget.org/packages/SkiaSharp/) and [SkiaSharp.Views.Maui.Controls](https://www.nuget.org/packages/SkiaSharp.Views.Maui.Controls/3.118.0-preview.2.3)
SkiaSharp is a cross-platform 2D graphics API for .NET platforms based on Google's Skia Graphics Library. 
```bash
$ dotnet add package SkiaSharp.Views.Maui.Controls --version 3.118.0-preview.2.3
$ dotnet add package SkiaSharp --version 3.116.1
$ dotnet add package SkiaSharp.Views.Forms --version 3.116.1
```

## Install [Gurobi Optimizer](https://www.nuget.org/packages/Gurobi.Optimizer)
```bash
$ dotnet add package Gurobi.Optimizer --version 12.0.1
```

# Remove a NuGet Package
```bash
$ dotnet list package
$ dotnet remove package Package_Name
```

# Workspace vs. Project vs. Solution [Doc](https://code.visualstudio.com/docs/csharp/project-management)

## Workspace [Doc](https://code.visualstudio.com/docs/editing/workspaces/workspaces)
A Visual Studio Code workspace is the collection of one or more folders that are opened in a VS Code window (instance). In most cases, you will have a single folder opened as the workspace. However, depending on your development workflow, you can include more than one folder, using an advanced configuration called Multi-root workspaces.

## Project
When you create a C# application in Visual Studio Code, you start with a project. A project contains all files (such as source code, images, etc.) that are compiled into an executable, library, or website.

## Solution
All of your related projects can then be stored in a container called a solution.

### Create a new solution
```bash
$ dotnet new solution
```

### Add project to a Solution

```bash
$ dotnet sln add YourProject.csproj
```

---
# Selected Theory

## [C# Quick Actions and Refactorings](https://code.visualstudio.com/docs/csharp/refactoring)