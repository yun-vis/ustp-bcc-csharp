---
# permalink: /about/
layout: single
title: "File IO"
classes: wide
header:
  image: /assets/images/teaser/teaser.png
  caption: "Image credit: [**Yun**](http://yun-vis.net)"  
last_modified_at: 2025-04-01
---

# Program Deployment

## Understanding .NET components

- **Deployment:** Software deployment is all of the activities that make a software system available for use.

- **Language Compilers:** These turn your source code written with languages C# into intermediate language (IL) code stored in assemblies.
With C# 6.0 and later, Microsoft switched to an open source rewritten compiler known as **Roslyn** that is also used by Visual Basic.

- **Assembly:** Assemblies form the fundamental units of deployment, version control, reuse, activation scoping, and security permissions for .NET-based applications. An assembly is a collection of types and resources that are built to work together and form a logical unit of functionality. Assemblies take the form of executable (.exe) or dynamic link library (.dll, so, .dylib) files, and are the building blocks of .NET applications. [Doc](https://docs.microsoft.com/en-us/dotnet/standard/assembly/)

- **Common Language Runtime (CLR):** This runtime loads assemblies, compiles
the IL code stored in them into native code instructions for your computer's CPU, and
executes the code within an environment that manages resources such as threads and
memory.

- **Package (Class Library) Manager:** A package manager or package-management system is a collection of software tools that automates the process of installing, upgrading, configuring, and removing computer programs for a computer in a consistent manner.

  - Packages can ship on their own schedule.
  - Packages can be tested independently of other packages.
  - Packages can support different OSes and CPUs by including multiple versions of the same assembly built for different OSes and CPUs.
  - Packages can have dependencies specific to only one library.
  - Apps are smaller because unreferenced packages aren't part of the distribution.

- **NuGet Packages:** NuGet is the package manager for .NET. Note that .NET is split into a set of packages, distributed using a Microsoft-supported package management technology named NuGet. [Doc](https://www.nuget.org/ )

- **Base Class Library (BCL):** The BCL provides the most foundational types and utility functionality and is the base of all other .NET class libraries. [Doc](https://docs.microsoft.com/en-us/dotnet/standard/framework-libraries)

- **Namespace:** A namespace is the address of a type. Namespaces are a mechanism to uniquely identify a type by requiring a full address rather than just a short name.

- **Dependency:** A dependency in programming is an essential functionality, library or piece of code that is essential for a different part of the code to work.

## Understanding the Microsoft .NET project SDKs

By default, console applications have a dependency reference on the Microsoft .NET SDK. This platform contains thousands of types in NuGet packages that almost all applications would need, such as the int and string types.

- **Software Development Kit (SDK):** A software development kit (SDK) is a collection of software development tools in one installable package.

- **Application Programming Interface (API):** An application programming interface is a connection between computers or between computer programs.

## Understanding Frameworks

There is a two-way relationship between frameworks and packages. Packages define the APIs, while frameworks group packages. A framework without any packages would not define
any APIs.

```csharp
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net6.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
  </PropertyGroup>

</Project>
```
```bash
$ cd C:\Program Files\dotnet\sdk // Windows 10
$ cd /usr/local/share/dotnet/sdk // MacOS
```

```csharp
using System;
// using System.Xml.Linq;

namespace MyBusiness
{
    class Program
    {
        static void Main(string[] args)
        {
            // XDocument doc = new XDocument();
            Stack<int> myStack = new Stack<int>();
        }
    }
}
```

# Publishing your Applications for Deployment

- Framework-dependent Deployment (FDD).
- Framework-dependent Executables (FDEs).
- Self-contained.

```csharp
using System;

namespace MyBusiness
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("I can run everywhere!");
            string? name = Console.ReadLine();
        }
    }
}
```

```csharp
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net6.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
    <RuntimeIdentifiers>
      win10-x64;osx-x64;rhel.7.4-x64
    </RuntimeIdentifiers>
  </PropertyGroup>
</Project>
```

- The win10-x64 RID value means Windows 10 or Windows Server 2016.
- The osx-x64 RID value means macOS High Sierra 10.13 or later.
- The rhel.7.4-x64 RID value means Red Hat Enterprise Linux (RHEL) 7.4 or later.

You can find the currently supported Runtime Identifier (RID) values from [Doc](https://docs.microsoft.com/en-us/dotnet/articles/core/rid-catalog).

## Understanding dotnet Commands

- dotnet restore: This downloads dependencies for the project.
- dotnet build: This compiles the project.
- dotnet test: This runs unit tests on the project.
- dotnet run: This runs the project.
- dotnet pack: This creates a NuGet package for the project.
- dotnet publish: This compiles and then publishes the project, either with dependencies
or as a self-contained application.
- dotnet add package: This adds a reference to a package or class library to the project.
```bash
$ dotnet add package Newtonsoft.Json --version 13.0.3
```
For example, if you want to add a package created by a third-party developer, for example,
[Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) from [nuget](https://www.nuget.org/).
- dotnet remove package: This removes a reference to a package or class library from the project.
- dotnet list package: This lists the package or class library references for the project.
```bash
$ dotnet list package
```

```csharp
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net6.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="13.0.3" />
  </ItemGroup>
</Project>
```

## Publishing a Self-Contained App

- **Debug Mode:** Debug includes debugging information in the compiled files (allowing easy debugging).
- **Release Mode:** Release usually has optimizations enabled.

```bash
$ dotnet publish -c Release -r osx-x64 --self-contained=true
```

## Publishing a Single-File App

```bash
$ dotnet publish -r osx-x64 -c Release --self-contained=false -p:PublishSingleFile=true
// The pdb is a program database file that stores debugging information.
```

## Packaging a Library for NuGet
```bash
$ dotnet build -c Release
$ dotnet pack -c Release
```

# Managing the Filesystem

## Internationalization

Internationalization is the process of enabling your code to run correctly all over the world. It has two parts: globalization and localization.

* Globalization is about writing your code to accommodate multiple languages and region
combinations (e.g., [Number Formating](https://learn.microsoft.com/en-us/globalization/locale/number-formatting), etc.). The combination of a language and a region is known as a culture.

* Localization is about customizing the user interface to support a language, for example,
changing the label of a button to be Close (en) or Fermer (fr).

* [ISO Language Code Table](https://lingohub.com/developers/supported-locales/language-designators-with-regions)

```csharp
using System;
using System.Globalization;

// main program
public class Program
{
    static void Main(string[] args)
    {
        // Set console encoding
        Console.WriteLine("Console.OutputEncoding = " + Console.OutputEncoding);
        Console.OutputEncoding = System.Text.Encoding.UTF8;

        CultureInfo globalization = CultureInfo.CurrentCulture;
        CultureInfo localization = CultureInfo.CurrentUICulture;
        Console.WriteLine("The current globalization culture is {0}: {1}",
        globalization.Name, globalization.DisplayName);
        Console.WriteLine("The current localization culture is {0}: {1}",
        localization.Name, localization.DisplayName);
        Console.WriteLine();
        Console.WriteLine("en-US: English (United States)");
        Console.WriteLine("da-DK: Danish (Denmark)");
        Console.WriteLine("fr-CA: French (Canada)");
        Console.WriteLine("de-AT: German (Austria)");
        Console.Write("Enter an ISO culture code: ");
        string? newCulture = Console.ReadLine();
        if (!string.IsNullOrEmpty(newCulture))
        {
            CultureInfo ci = new CultureInfo(newCulture);
            CultureInfo.CurrentCulture = ci;
            CultureInfo.CurrentUICulture = ci;
        }
        Console.WriteLine();
        Console.Write("Enter your name: ");
        string? name = Console.ReadLine();
        Console.Write("Enter your date of birth: ");
        string? dob = Console.ReadLine();
        Console.Write("Enter your salary: ");
        string? salary = Console.ReadLine();
        if (dob != null && salary != null)
        {
            DateTime date = DateTime.Parse(dob);
            int minutes = (int)DateTime.Today.Subtract(date).TotalMinutes;
            decimal earns = decimal.Parse(salary);
            Console.WriteLine("{0} was born on a {1:dddd}, is {2:N0} minutes old, and earns {3:C}", name, date, minutes, earns);
        }
    }
}
```

```bash
$ The current globalization culture is en-US: English (United States)
$ The current localization culture is en-US: English (United States) 

$ en-US: English (United States)
$ fr-CA: French (Canada)
$ de-AT: German (Austria)
$ Enter an ISO culture code: de-At

$ Enter your name: Yun
$ Enter your date of birth: 19/8/1999
$ Enter your salary: 230000
$ Yun was born on a Donnerstag, is 12 402 720 minutes old, and earns € 230.000,00
```

## Handling cross-platform environments and filesystems

```csharp
using System.IO; // types for managing the filesystem
using static System.Console;
using static System.IO.Directory;
using static System.IO.Path;
using static System.Environment;

namespace MyBusiness
{
    class Program
    {
        static void Main(string[] args)
        {
            OutputFileSystemInfo();
        }
        static void OutputFileSystemInfo()
        {
            WriteLine("{0,-33} {1}", "Path.PathSeparator", PathSeparator);
            WriteLine("{0,-33} {1}", "Path.DirectorySeparatorChar",
              DirectorySeparatorChar);
            WriteLine("{0,-33} {1}", "Directory.GetCurrentDirectory()",
              GetCurrentDirectory());
            WriteLine("{0,-33} {1}", "Environment.CurrentDirectory",
              CurrentDirectory);
            WriteLine("{0,-33} {1}", "Environment.SystemDirectory",
              SystemDirectory);
            WriteLine("{0,-33} {1}", "Path.GetTempPath()", GetTempPath());
            WriteLine("GetFolderPath(SpecialFolder");
            WriteLine("{0,-33} {1}", " .System)",
              GetFolderPath(SpecialFolder.System));
            WriteLine("{0,-33} {1}", " .ApplicationData)",
              GetFolderPath(SpecialFolder.ApplicationData));
            WriteLine("{0,-33} {1}", " .MyDocuments)",
              GetFolderPath(SpecialFolder.MyDocuments));
            WriteLine("{0,-33} {1}", " .Personal)",
              GetFolderPath(SpecialFolder.Personal));
        }
    }
}
```
On Windows
```bash
$ Path.PathSeparator                ;
$ Path.DirectorySeparatorChar       \
$ Directory.GetCurrentDirectory()   C:\Users\lbwu\Dropbox\FH\BCC\C-Sharp\Codes\CRC_CSD-09\MyBusiness
$ Environment.CurrentDirectory      C:\Users\lbwu\Dropbox\FH\BCC\C-Sharp\Codes\CRC_CSD-09\MyBusiness
$ Environment.SystemDirectory       C:\Windows\system32
$ Path.GetTempPath()                C:\Users\lbwu\AppData\Local\Temp\
$ GetFolderPath(SpecialFolder
$  .System)                         C:\Windows\system32
$  .ApplicationData)                C:\Users\lbwu\AppData\Roaming
$  .MyDocuments)                    C:\Users\lbwu\Documents
$  .Personal)                       C:\Users\lbwu\Documents
```
On MacOS
```bash
$ Path.PathSeparator                :
$ Path.DirectorySeparatorChar       /
$ Directory.GetCurrentDirectory()   /Users/yun/Dropbox/FH/BCC/C-Sharp/Codes/CRC_CSD-09/MyBusiness
$ Environment.CurrentDirectory      /Users/yun/Dropbox/FH/BCC/C-Sharp/Codes/CRC_CSD-09/MyBusiness
$ Environment.SystemDirectory       /System
$ Path.GetTempPath()                /var/folders/y_/jv3nd6kn7_v88vmf3378p6p40000gn/T/
$ GetFolderPath(SpecialFolder
$  .System)                         /System
$  .ApplicationData)                /Users/yun/.config
$  .MyDocuments)                    /Users/yun
$  .Personal)                       /Users/yun
```

## Managing drives

```csharp
using System.IO; // types for managing the filesystem
using static System.Console;
using static System.IO.Directory;
using static System.IO.Path;
using static System.Environment;

namespace MyBusiness
{
    class Program
    {
        static void Main(string[] args)
        {
            WorkWithDrives();
        }
        static void WorkWithDrives()
        {
            WriteLine("{0,-30} | {1,-10} | {2,-7} | {3,18} | {4,18}",
              "NAME", "TYPE", "FORMAT", "SIZE (BYTES)", "FREE SPACE");
            foreach (DriveInfo drive in DriveInfo.GetDrives())
            {
                if (drive.IsReady)
                {
                    WriteLine(
                            "{0,-30} | {1,-10} | {2,-7} | {3,18:N0} | {4,18:N0}",
                            drive.Name, drive.DriveType, drive.DriveFormat,
                            drive.TotalSize, drive.AvailableFreeSpace);
                }
                else
                {
                    WriteLine("{0,-30} | {1,-10}", drive.Name, drive.DriveType);
                }
            }
        }
    }
}
```
On Windows
```bash
$ NAME                           | TYPE       | FORMAT  |       SIZE (BYTES) |         FREE SPACE
$ C:\                            | Fixed      | NTFS    |  1,023,551,021,056 |    776,903,106,560
$ H:\                            | Network    | NTFS    |      2,147,483,648 |      2,147,479,552
$ I:\                            | Network    | NTFS    |  6,596,932,399,104 |    260,713,881,600
$ M:\                            | Network    | NTFS    |     53,687,091,200 |     53,687,091,200
$ P:\                            | Network    | NTFS    |  2,199,005,425,664 |    834,980,163,584
$ S:\                            | Network    | NTFS    |  6,596,932,399,104 |    260,713,881,600
```
On MacOS
```bash
$ NAME                           | TYPE       | FORMAT  |       SIZE (BYTES) |         FREE SPACE
$ /                              | Fixed      | apfs    |    500,068,036,608 |      6,828,941,312
$ /dev                           | Ram        | devfs   |            194,048 |                  0
$ /private/var/vm                | Fixed      | apfs    |    500,068,036,608 |      6,828,941,312
$ /net                           | Network    | autofs  |                  0 |                  0
$ /home                          | Network    | autofs  |                  0 |                  0
$ /Volumes/firmwaresyncd.J9xOfG  | Fixed      | msdos   |        206,472,192 |        182,210,048
```

## Managing directories

```csharp
using System.IO; // types for managing the filesystem
using static System.Console;
using static System.IO.Directory;
using static System.IO.Path;
using static System.Environment;

namespace MyBusiness
{
    class Program
    {
        static void Main(string[] args)
        {
            WorkWithDirectories();
        }
        static void WorkWithDirectories()
        {
            // define a directory path for a new folder 
            // starting in the user's folder
            // SpecialFolder.Personal is defined differently on Windows and MacOS
            string newFolder = Combine(
                GetFolderPath(SpecialFolder.Desktop), "MyNewFolder");

            Console.WriteLine("Working with:" + newFolder);
            // check if it exists
            WriteLine($"Does it exist? {Exists(newFolder)}");
            // create directory
            WriteLine("Creating it...");
            CreateDirectory(newFolder);
            WriteLine($"Does it exist? {Exists(newFolder)}");
            Write("Confirm the directory exists, and then press ENTER: ");
            ReadLine();
            // delete directory
            WriteLine("Deleting it...");
            Delete(newFolder, recursive: true);
            WriteLine($"Does it exist? {Exists(newFolder)}");
        }
    }
}
```
```bash
$ Working with: /Users/yun/Desktop/MyNewFolder
$ Does it exist? False
$ Creating it...
$ Does it exist? True
$ Confirm the directory exists, and then press ENTER:
$ Deleting it...
$ Does it exist? False
```

## Managing files

```csharp
using System.IO; // types for managing the filesystem
using static System.Console;
using static System.IO.Directory;
using static System.IO.Path;
using static System.Environment;

namespace MyBusiness
{
    class Program
    {
        static void Main(string[] args)
        {
            WorkWithFiles();
        }
        static void WorkWithFiles()
        {
            // define a directory path to output files // starting in the user's folder
            string dir = Combine(
                GetFolderPath(SpecialFolder.Personal),
                "Desktop", "MyNewFiles");
            CreateDirectory(dir);
            // define file paths
            string textFile = Combine(dir, "Dummy.txt");
            string backupFile = Combine(dir, "Dummy.bak");
            WriteLine($"Working with: {textFile}");
            // check if a file exists
            WriteLine($"Does it exist? {File.Exists(textFile)}");
            // create a new text file and write a line to it
            StreamWriter textWriter = File.CreateText(textFile);
            textWriter.WriteLine("Hello, C#!");
            textWriter.Close(); // close file and release resources
            WriteLine($"Does it exist? {File.Exists(textFile)}");
                                // copy the file, and overwrite if it already exists
            File.Copy(sourceFileName: textFile,
              destFileName: backupFile, overwrite: true);
            WriteLine(
              $"Does {backupFile} exist? {File.Exists(backupFile)}");
            Write("Confirm the files exist, and then press ENTER: ");
            ReadLine();
            // delete file
            File.Delete(textFile);
            WriteLine($"Does it exist? {File.Exists(textFile)}");
            // read from the text file backup
            WriteLine($"Reading contents of {backupFile}:");
            StreamReader textReader = File.OpenText(backupFile);
            WriteLine(textReader.ReadToEnd());
            textReader.Close();
        }
    }
}
```
```bash
$ Working with: /Users/yun/Desktop/MyNewFiles/Dummy.txt
$ Does it exist? False
$ Does /Users/yun/Desktop/MyNewFiles/Dummy.bak exist? True
$ Confirm the files exist, and then press ENTER:
$ Does it exist? False
$ Reading contents of /Users/yun/Desktop/MyNewFiles/Dummy.bak:
$ Hello, C#!
```

## Managing paths

```csharp
// Managing paths
WriteLine($"Folder Name: {GetDirectoryName(textFile)}");
WriteLine($"File Name: {GetFileName(textFile)}");
WriteLine("File Name without Extension: {0}",
  GetFileNameWithoutExtension(textFile));
WriteLine($"File Extension: {GetExtension(textFile)}");
WriteLine($"Random File Name: {GetRandomFileName()}");
WriteLine($"Temporary File Name: {GetTempFileName()}");
```

On Windows
```bash
$ Folder Name: C:\Users\lbwu\Documents\Desktop\MyNewFiles
$ File Name: Dummy.txt
$ File Name without Extension: Dummy
$ File Extension: .txt
$ Random File Name: thi4osvc.sk0
$ Temporary File Name: C:\Users\lbwu\AppData\Local\Temp\tmpD3BF.tmp
```

On MacOS
```bash
$ Folder Name: /Users/yun/Desktop/MyNewFiles
$ File Name: Dummy.txt
$ File Name without Extension: Dummy
$ File Extension: .txt
$ Random File Name: qh4j5vy2.kgn
$ Temporary File Name: /var/folders/y_/jv3nd6kn7_v88vmf3378p6p40000gn/T/tmpfQQNS0.tmp
```

## Getting file information

```csharp
FileInfo info = new FileInfo(backupFile);
WriteLine($"{backupFile}:");
WriteLine($"Contains {info.Length} bytes");
WriteLine($"Last accessed {info.LastAccessTime}");
WriteLine($"Has readonly set to {info.IsReadOnly}");
```

On Windows
```bash
$ C:\Users\lbwu\Documents\Desktop\MyNewFiles\Dummy.bak:
$ Contains 12 bytes
$Last accessed 4/13/2023 9:11:26 PM
$ Has readonly set to False
```

On MacOS
```bash
$ /Users/yun/Desktop/MyNewFiles/Dummy.bak:
$ Contains 11 bytes
$ Last accessed 3/30/2022 8:44:26 AM
$ Has readonly set to False
```

## Reading and writing with streams

```csharp
using System.IO; // types for managing the filesystem
using static System.Console;
using static System.IO.Directory;
using static System.IO.Path;
using static System.Environment;

namespace MyBusiness
{
    class Program
    {
        static void Main(string[] args)
        {
            WorkWithText();
        }
        // define an array of cat types
        static string[] cattypes = new string[] {
            "SiameseCat", "BritishShorthair", "MaineCoon", "PersianCat", "Ragdoll", "SphynxCat" };
        static void WorkWithText()
        {
            // define a file to write to
            string textFile = Combine(CurrentDirectory, "streams.txt");
            // create a text file and return a helper writer
            StreamWriter text = File.CreateText(textFile);
            // enumerate the strings, writing each one
            // to the stream on a separate line
            foreach (string item in cattypes)
            {
                text.WriteLine(item);
            }
            text.Close(); // release resources
                          // output the contents of the file
            WriteLine("{0} contains {1:N0} bytes.",
              arg0: textFile,
              arg1: new FileInfo(textFile).Length);
            WriteLine(File.ReadAllText(textFile));
        }
    }
}
```
```bash
/Users/yun/Dropbox/FH/BCC/C-Sharp/Codes/CRC_CSD-09/MyBusiness/streams.txt contains 73 bytes.
$ SiameseCat
$ BritishShorthair
$ MaineCoon
$ PersianCat
$ Ragdoll
$ SphynxCat
```

### The magic item calculator example using files
```csharp
using System;
using System.Collections.Generic;
using System.IO;

class BaseWeapon
{
    public int BaseDamage { get; set; }
    public double AttackSpeed { get; set; }

    public double CalculateDPS(DamageModifier damageModifier, double durationInSeconds)
    {
        int attackCount = (int)(durationInSeconds / AttackSpeed);
        double totalDamage = 0;

        for (int i = 0; i < attackCount; i++)
        {
            totalDamage += damageModifier(BaseDamage);
        }

        return totalDamage / durationInSeconds;
    }
    
    public static Dictionary<string, BaseWeapon> LoadWeaponsFromCSV(string filePath)
    {
        var weapons = new Dictionary<string, BaseWeapon>();

        string[] lines = File.ReadAllLines(filePath);

        foreach (var line in lines[1..]) // Skip header line
        {
            var parts = line.Split(',');
            weapons[parts[0]] = new BaseWeapon
            {
                BaseDamage = int.Parse(parts[1]),
                AttackSpeed = double.Parse(parts[2])
            };
        }

        return weapons;
    }
}

delegate int DamageModifier(int baseDamage);

class Program
{
    

    static void Main()
    {
        var weapons = BaseWeapon.LoadWeaponsFromCSV("weapons.csv");

        int strength = 10;
        Random rng = new();

        Dictionary<string, DamageModifier> modifiers = new()
        {
            ["giant"] = dmg => dmg + strength,
            ["random"] = dmg => dmg * rng.Next(0, 3) * 2,
            ["brutal"] = dmg => (dmg * dmg) / 5
        };

        var itemModifiers = new List<string> {"random" };
        string baseWeaponName = "Sword";

        DamageModifier calculateDamage = dmg => dmg;
        foreach (var mod in itemModifiers)
        {
            if (modifiers.ContainsKey(mod))
            {
                DamageModifier modFunc = modifiers[mod];
                DamageModifier previousFunc = calculateDamage;
                calculateDamage = dmg => modFunc(previousFunc(dmg));
            }
        }

        var dps = weapons[baseWeaponName].CalculateDPS(calculateDamage, 100000);

        using var writer = new StreamWriter("dps.txt", append: true);
        writer.WriteLine($"Final DPS for {string.Join(" ", itemModifiers)} {baseWeaponName}: {dps}");
    }
}
```

Example weapons.csv
```csv
Name,Damage,AttackSpeed
Sword,10,1.5
Axe,20,2.0
Dagger,5,0.5
```

How to force a certain file to be put into the built folder:
```xml
<ItemGroup>
  <None Update="weapons.csv">
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
  </None>
</ItemGroup>
```

## Encoding strings as byte arrays

```csharp
using static System.Console;
using System.Text;

namespace MyBusiness
{
    class Program
    {
        static void Main(string[] args)
        {
            WorkWithText();
        }
        static void WorkWithText()
        {
            WriteLine("Encodings");
            WriteLine("[1] ASCII");
            WriteLine("[2] UTF-7");
            WriteLine("[3] UTF-8");
            WriteLine("[4] UTF-16 (Unicode)");
            WriteLine("[5] UTF-32");
            WriteLine("[any other key] Default");
            // choose an encoding
            Write("Press a number to choose an encoding: ");
            ConsoleKey number = ReadKey(intercept: false).Key;
            WriteLine();
            WriteLine();
            Encoding encoder = number switch
            {
                ConsoleKey.D1 => Encoding.ASCII,
                ConsoleKey.D2 => Encoding.UTF7,
                ConsoleKey.D3 => Encoding.UTF8,
                ConsoleKey.D4 => Encoding.Unicode,
                ConsoleKey.D5 => Encoding.UTF32,
                _ => Encoding.Default
            };
            // define a string to encode
            string message = "A pint of milk is £1.99";
            // encode the string into a byte array
            byte[] encoded = encoder.GetBytes(message);
            // check how many bytes the encoding needed
            WriteLine("{0} uses {1:N0} bytes.",
              encoder.GetType().Name, encoded.Length);
            // enumerate each byte
            WriteLine($"BYTE HEX CHAR");
            foreach (byte b in encoded)
            {
                WriteLine($"{b,4} {b.ToString("X"),4} {(char)b,5}");
            }
            // decode the byte array back into a string and display it
            string decoded = encoder.GetString(encoded);
            WriteLine(decoded);
        }
    }
}
```
```bash
$ Encodings
$ [1] ASCII
$ [2] UTF-7
$ [3] UTF-8
$ [4] UTF-16 (Unicode)
$ [5] UTF-32
$ [any other key] Default
$ Press a number to choose an encoding: 1

$ ASCIIEncodingSealed uses 23 bytes.
$ BYTE HEX CHAR
$   65   41     A
$   32   20      
$  112   70     p
$  105   69     i
$  110   6E     n
$  116   74     t
$   32   20      
$  111   6F     o
$  102   66     f
$   32   20      
$  109   6D     m
$  105   69     i
$  108   6C     l
$  107   6B     k
$   32   20      
$  105   69     i
$  115   73     s
$   32   20      
$   63   3F     ?
$   49   31     1
$   46   2E     .
$   57   39     9
$   57   39     9
$ A pint of milk is ?1.99
```

## XML Streams

In MyBusiness/Program.cs,
```csharp
// System libraries
using System; // DateTime

// External libraries
using AnimalLibrary;

namespace MyBusiness;

class Program
{
    static void Main(string[] args)
    {
        // create an object list
        // M refers to the decimal type
        List<Person> people = new List<Person> {
            new Person(30000M) {
                FirstName = "Alice",
                LastName = "Smith",
                DateOfBirth = new DateTime(1974, 3, 14)
                },
            new Person(40000M) {
                FirstName = "Bob",
                LastName = "Jones",
                DateOfBirth = new DateTime(1969, 11, 23)
                },
            new Person(20000M) {
                FirstName = "Charlie",
                LastName = "Cox",
                DateOfBirth = new DateTime(1984, 5, 4),
                Children = new HashSet<Person> {
                    new Person(0M) { FirstName = "Sally",
                    LastName = "Cox",
                    DateOfBirth = new DateTime(2000, 7, 12)}
                    }
                }
            };

        // Stream 
        StreamXML streamXML = new StreamXML();
        streamXML.Reader(people, "people.xml");
        streamXML.Writer(people, "stream_new.xml");
    }
}
```

In AnimalLibrary/Person.cs,
```csharp
namespace AnimalLibrary;

public class Person
{
    // Default constructor
    public Person()
    {
    }

    // Paramerterized constructor
    public Person(decimal initialSalary)
    {
        Salary = initialSalary;
    }

    // Properties
    public string? FirstName { get; set; }
    public string? LastName { get; set; }
    public DateTime DateOfBirth { get; set; }
    public HashSet<Person>? Children { get; set; }
    // Note that System.Xml.Serialization only serializes public properties
    // and fields. The Salary property is not serialized because it is protected.
    internal protected decimal Salary { get; set; }
}
```

In AnimalLibrary/StreamXML.cs,
```csharp
using System.Xml;
using static System.Environment; // CurrentDirectory
using static System.IO.Path; // Combine

namespace AnimalLibrary;

public class StreamXML
{
    // Default constructor
    public StreamXML()
    {
    }

    // Methods
    public void Reader(List<Person> people, string filename)
    {
        people = new List<Person>();

        // create a file to write to
        string file = Combine(CurrentDirectory, filename);

        using (XmlReader reader = XmlReader.Create(file))
        {
            while (reader.Read())
            {
                if (reader.IsStartElement() && reader.Name == "Person")
                {
                    var person = ReadPerson(reader);
                    people.Add(person);
                }
            }
        }

        if (people != null)
        {
            foreach (Person item in people)
            {
                if (item.Children != null)
                {
                    Console.WriteLine("{0} has {1} children.",
                        item.LastName, item.Children.Count);
                }
            }
        }
    }

    static Person ReadPerson(XmlReader reader)
    {
        // Initialization
        Person person = new Person();
        person.Children = new HashSet<Person>();

        // Read the XML node and its attributes
        while (reader.Read())
        {
            if (reader.NodeType == XmlNodeType.EndElement && reader.Name == "Person")
                break;

            if (reader.IsStartElement())
            {
                switch (reader.Name)
                {
                    case "FirstName":
                        person.FirstName = reader.ReadElementContentAsString();
                        break;
                    case "LastName":
                        person.LastName = reader.ReadElementContentAsString();
                        break;
                    case "DateOfBirth":
                        person.DateOfBirth = reader.ReadElementContentAsDateTime();
                        break;
                    case "Salary":
                        person.Salary = reader.ReadElementContentAsDecimal();
                    break;
                    case "Children":
                        while (reader.Read())
                        {
                            if (reader.NodeType == XmlNodeType.EndElement && reader.Name == "Children")
                                break;

                            if (reader.IsStartElement() && reader.Name == "Person")
                            {
                                Person child = ReadPerson(reader);
                                person.Children.Add(child);
                            }
                        }
                        break;
                }
            }
        }

        return person;
    }

    public void Writer(List<Person> people, string filename)
    {
        // create a file to write to
        string file = Combine(CurrentDirectory, filename);

        // create a file stream
        // using allows us not to forget stream.Close();
        using (FileStream xmlFileStream = File.Create(file))
        {
            using (XmlWriter writer = XmlWriter.Create(xmlFileStream, new XmlWriterSettings { Indent = true }))
            {
                writer.WriteStartDocument();
                writer.WriteStartElement("People");

                foreach (var person in people)
                {
                    WritePerson(writer, person);
                }

                writer.WriteEndElement(); // People
                writer.WriteEndDocument();
            }
        }

        Console.WriteLine("Written {0:N0} bytes of XML to {1}",
            arg0: new FileInfo(file).Length,
            arg1: file);
        Console.WriteLine();
        // Display the serialized object graph
        Console.WriteLine(File.ReadAllText(file));
    }

    static void WritePerson(XmlWriter writer, Person person)
    {
        writer.WriteStartElement("Person");

        writer.WriteElementString("FirstName", person.FirstName);
        writer.WriteElementString("LastName", person.LastName);
        // "s" format specifier is used for sortable date/time pattern.
        writer.WriteElementString("DateOfBirth", person.DateOfBirth.ToString("s"));
        // writer.WriteElementString("Salary", person.Salary.ToString());

        if (person.Children != null && person.Children.Count > 0)
        {
            writer.WriteStartElement("Children");
            foreach (var child in person.Children)
            {
                WritePerson(writer, child); // recursive call for nested children
            }
            writer.WriteEndElement(); // Children
        }

        writer.WriteEndElement(); // Person
    }
}
```

## Serializing Objects

- **Serialization:** is the process of converting a live object into a sequence of bytes using a specified format.
- **Deserialization:** is the reverse process of **Serialization**.

There are dozens of formats you can specify, but the two most common ones are **eXtensible Markup Language (XML)** and **JavaScript Object Notation (JSON)**.

In MyBusiness/Program.cs,
```csharp
// System libraries
using System; // DateTime

// External libraries
using AnimalLibrary;
using GraphLibrary;

namespace MyBusiness;

class Program
{
    static void Main(string[] args)
    {
        // create an object list
        // M refers to the decimal type
        List<Person> people = new List<Person> {
            new Person(30000M) {
                FirstName = "Alice",
                LastName = "Smith",
                DateOfBirth = new DateTime(1974, 3, 14)
                },
            new Person(40000M) {
                FirstName = "Bob",
                LastName = "Jones",
                DateOfBirth = new DateTime(1969, 11, 23)
                },
            new Person(20000M) {
                FirstName = "Charlie",
                LastName = "Cox",
                DateOfBirth = new DateTime(1984, 5, 4),
                Children = new HashSet<Person> {
                    new Person(0M) { FirstName = "Sally",
                    LastName = "Cox",
                    DateOfBirth = new DateTime(2000, 7, 12)}
                    }
                }
            };

        // Stream 
        // StreamXML streamXML = new StreamXML();
        // streamXML.Reader(people, "people.xml");
        // streamXML.Writer(people, "stream_new.xml");

        // Serialization
        SerializeXML serializeXML = new SerializeXML();
        serializeXML.Reader(people, "people.xml");
        serializeXML.Writer(people, "people_new.xml");
    }

}
```
```bash
<?xml version="1.0" encoding="utf-8"?>
<ArrayOfPerson xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <Person>
    <FirstName>Alice</FirstName>
    <LastName>Smith</LastName>
    <DateOfBirth>1974-03-14T00:00:00</DateOfBirth>
  </Person>
  <Person>
    <FirstName>Bob</FirstName>
    <LastName>Jones</LastName>
    <DateOfBirth>1969-11-23T00:00:00</DateOfBirth>
  </Person>
  <Person>
    <FirstName>Charlie</FirstName>
    <LastName>Cox</LastName>
    <DateOfBirth>1984-05-04T00:00:00</DateOfBirth>
    <Children>
      <Person>
        <FirstName>Sally</FirstName>
        <LastName>Cox</LastName>
        <DateOfBirth>2000-07-12T00:00:00</DateOfBirth>
      </Person>
    </Children>
  </Person>
</ArrayOfPerson>
```

- [using statement - ensure the correct use of disposable objects](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/using)
- [standard-numeric-format-strings](https://learn.microsoft.com/en-us/dotnet/standard/base-types/standard-numeric-format-strings)
- [Composite formatting](https://learn.microsoft.com/en-us/dotnet/standard/base-types/composite-formatting)
- [DateTime.ToString Method](https://learn.microsoft.com/en-us/dotnet/api/system.datetime.tostring)
- [Standard date and time format strings](https://learn.microsoft.com/en-us/dotnet/standard/base-types/standard-date-and-time-format-strings)

## Serializing as XML and Deserializing XML files

```csharp
using System.Xml.Serialization; // XmlSerializer
using static System.Environment; // CurrentDirectory
using static System.IO.Path; // Combine

namespace AnimalLibrary;

public class SerializeXML
{
    // Default constructor
    public SerializeXML()
    {
    }

    // Methods
    public void Reader(List<Person>? people, string filename)
    {
        // create object that will format a List of Persons as XML
        XmlSerializer xs = new XmlSerializer(typeof(List<Person>));
        // create a file to read from
        string file = Combine(CurrentDirectory, filename);

        using (FileStream xmlLoad = File.Open(file, FileMode.Open))
        {
            // deserialize and cast the object graph into a List of Person
            people = (List<Person>?)xs.Deserialize(xmlLoad);
            if (people != null)
            {
                foreach (Person item in people)
                {
                    if (item.Children != null)
                    {
                        Console.WriteLine("{0} has {1} children.",
                            item.LastName, item.Children.Count);
                    }
                }
            }
        }
    }

    public void Writer(List<Person> people, string filename)
    {
        // create object that will format a List of Persons as XML
        XmlSerializer xs = new XmlSerializer(typeof(List<Person>));
        // create a file to write to
        string file = Combine(CurrentDirectory, filename);

        // using allows us not to forget stream.Close();
        using (FileStream stream = File.Create(file))
        {
            // serialize the object graph to the stream
            xs.Serialize(stream, people);
        }

        // The compiler converts above to:
        // try-catch-finally statement
        // The try-catch statement consists of a try block followed by one or 
        // more catch clauses, which specify handlers for different exceptions.
        // FileStream stream = File.Create(file);
        // try
        // {
        //     // serialize the object graph to the stream
        //     xs.Serialize(stream, people);
        // }
        // catch (Exception ex)
        // {
        //     Console.WriteLine($"{ex.GetType()} says {ex.Message}");
        // }
        // finally
        // {
        //     // if stream is not null, we close it
        //     if (stream != null) stream.Dispose();
        // }

        Console.WriteLine("Written {0:N0} bytes of XML to {1}",
          arg0: new FileInfo(file).Length,
          arg1: file);
        Console.WriteLine();
        // Display the serialized object graph
        Console.WriteLine(File.ReadAllText(file));
    }
}
```
```bash
$ Smith has 0 children.
$ Jones has 0 children.
$ Cox has 1 children.
```

## Taking Care of System-Dependent Methods [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.environment.specialfolder?view=net-6.0)

```csharp
using System;

namespace MyBusiness
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.Write("My operating system (OS) is ");
            Console.WriteLine(Environment.OSVersion);
            Console.Write("Is my OS a Mac? ");            
            Console.WriteLine(OperatingSystem.IsMacOS());
            // Console.WriteLine(OperatingSystem.IsWindows());            
            // Console.WriteLine(OperatingSystem.IsLinux());
            Console.Write("Environment.SpecialFolder.Personal = ");
            Console.WriteLine(Environment.GetFolderPath(Environment.SpecialFolder.Personal));
            Console.Write("Environment.SpecialFolder.UserProfile = ");
            Console.WriteLine(Environment.GetFolderPath(Environment.SpecialFolder.UserProfile));
        }
    }
}
```
On Windows
```bash
My operating system (OS) is Microsoft Windows NT 10.0.19044.0
Is my OS a Mac? False
Environment.SpecialFolder.Personal = C:\Users\lbwu\Documents
Environment.SpecialFolder.UserProfile = C:\Users\lbwu
```
On MacOS
```bash
My operating system (OS) is Unix 10.14.6
Is my OS a Mac? True
Environment.SpecialFolder.Personal = /Users/yun
Environment.SpecialFolder.UserProfile = /Users/yun
```

---
# Selected Theory

* [Numerals in various writing systems](https://omniglot.com/language/numerals.htm)

# File System
