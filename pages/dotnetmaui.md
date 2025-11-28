---
# permalink: /about/
layout: single
title: ".Net NAUI"
classes: wide
header:
  image: /assets/images/teaser/teaser.png
  caption: "Image credit: [**Yun**](http://yun-vis.net)"
last_modified_at: 2025-02-06
---

# [Optional]
# .NET Multi-platform App UI (MAUI)

# .NET Workload
Workloads are slices of the first party dotnet SDK that have been split off to keep the installation smaller. As in you don't need the Android toolchain if you never develop for Android. Nothing is stopping you from shipping your own SDK.

# Install MAUI Workload
```bash
// Install MAUI workload.
$ dotnet workload install maui
// Check what workloads are installed.
$ dotnet workload list
// Check if there are other workloads can be installed.
$ dotnet workload search 
```

# Create your first App
```bash
// Show new project list
$ dotnet new list
// For more information
$ dotnet new list -h
// Create a MAUI project
// Alternatively, you can create a MAUI project from VS Code Explorer or Command Palette
$ dotnet new maui
```

# Before Moving On

## Some Terminology

### What is XAML?
XAML (i.e., Extensible Application Markup Language) is XML-based markup language that is used to define the user interface in .Net Applications. There are three XAML files that are included in the project template, which are App.xaml, AppShell.xaml, MainPage.xaml. These files are platform agnostic. Each XAML file is in pair with the C# file, which is a code-behind file associated with the XAML file.
### MauiProgram.cs class
MauiProgram.cs class provides the entry point for the application.
### What is partial class?
### [MVVM (Model-View-ViewModel)](https://learn.microsoft.com/en-us/dotnet/architecture/maui/mvvm#the-mvvm-pattern)
There are three core components in the MVVM pattern: the model, the view, and the view model. Each serves a distinct purpose. The diagram below shows the relationships between the three components.

# Install Xcode/iOS/Java SDK/Andriod SDK (Also in the Output)
Check the prerequisites on [installation instruction](https://learn.microsoft.com/en-us/dotnet/maui/get-started/installation?view=net-maui-9.0&viewFallbackFrom=net-maui-8.0&tabs=visual-studio-code#prerequisites) of MAUI.

Andriod SDK as an example:
```bash
$ dotnet build -t:InstallAndroidDependencies -f:net8.0-android -p:AndroidSdkDirectory="/path/to/sdk" -p:AcceptAndroidSDKLicenses=True
```

# Run the First Windows App
* Click on the main file: MainPage.xaml.cs
* Ctrl+Shift+P to enable the vscode Command Palette and run the command ".NET MAUI: Pick Windows Device".

```csharp

```

---
# External Resources

* [.NET Multi-platform App UI documentation](https://learn.microsoft.com/en-us/dotnet/maui/?view=net-maui-8.0)

* [Awesome .NET MAUI](https://github.com/jsuarezruiz/awesome-dotnet-maui)

* [.NET MAUI Learning Resources](https://github.com/jfversluis/learn-dotnet-maui)
  
* [Getting Started with MAUI in Visual Studio Code on Mac](https://learn.microsoft.com/en-us/shows/visual-studio-toolbox/getting-started-with-maui-in-visual-studio-code)