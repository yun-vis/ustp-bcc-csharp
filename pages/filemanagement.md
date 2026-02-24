---
# permalink: /about/
layout: single
title: "File Management"
classes: wide
header:
  image: /assets/images/teaser/teaser.png
  caption: "Image credit: [**Yun**](http://yun-vis.net)"  
last_modified_at: 2026-02-24
---

# Other Properties of Methods
## Types of the Methods
* **Instance methods** are actions that an object does to itself.
  * A mom cat procreates a kitty by taking a dad cat as an input.
  * The mom cat cannot produce kitties from multiple dad cats.
* **Static methods** are actions the type does.
  * The owner of the cats encourages them to procreate a kitty.
  * The owner can pair many cat couples at the same time.

```csharp
using Animals;

namespace program
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create 3 cats and initialize them
            Cat[] cats = {
                new Cat("Nana", new DateTime(2019, 12, 9)),
                new Cat("Coffee", new DateTime(2019, 6, 20)),
                new Cat("Kiwi", new DateTime(2018, 11, 19))
            };

            // Print out the present content
            foreach (Cat cat in cats)
            {
                cat.WriteToConsole();
            }

            // Call instance method
            Cat kitty1 = cats[0].ProduceKittyWith(cats[1]);
            kitty1.Name = "Naffee";
            // Call static method
            Cat kitty2 = Cat.ProduceKitty(cats[2], cats[1]);
            // The following statement functions as the above one
            // Cat kitty2 = kiwi * coffee;
            kitty2.Name = "Kiffee";

            // Print out the kitty name
            foreach (Cat cat in cats)
            {
                Console.WriteLine($"{cat.Name} has {cat.Children.Count} kitty.");
            }
            Console.WriteLine(
            format: "{0}'s first kitty is named \"{1}\".",
            arg0: cats[1].Name,
            arg1: cats[1].Children[0].Name);
        }
    }
}

/*
The animal namespace
*/
namespace Animals
{
    public class Cat
    {
        /*
        Class field, including different variables
        they can be organized by similar characteristics
        */

        // The name of the cat
        public string Name;
        // The birthday of the cat
        public DateTime DateOfBirth;
        // The children of the cat
        public List<Cat> Children = new List<Cat>();

        /*
        Class methods, where functions should be implemented
        */

        // Constructors
        // Default constructor. It will be called by default
        public Cat()
        {
            Name = "UnknownCat";
            DateOfBirth = DateTime.Today;
        }
        // Parameterized Constructor
        public Cat(string name, DateTime dateOfBirth)
        {
            this.Name = name;
            this.DateOfBirth = dateOfBirth;
        }
        // Finalizer/Desctructor
        ~Cat()
        {
        }

        // Print out method
        public void WriteToConsole()
        {
            Console.WriteLine($"{Name} was born on a {DateOfBirth:dddd}.");
        }

        // Static method to "multiply"
        public static Cat ProduceKitty(Cat cat1, Cat cat2)
        {
            Cat kitty = new Cat
            {
                Name = $"Baby of {cat1.Name} and {cat2.Name}"
            };
            cat1.Children.Add(kitty);
            cat2.Children.Add(kitty);
            return kitty;
        }

        // Use operators instead of the above method
        public static Cat operator *(Cat cat1, Cat cat2)
        {
            return Cat.ProduceKitty(cat1, cat2);
        }

        // Instance method to "multiply"
        public Cat ProduceKittyWith(Cat partner)
        {
            return ProduceKitty(this, partner);
        }
    }
}
```
```bash
$ Nana was born on a Monday.
$ Coffee was born on a Thursday.
$ Kiwi was born on a Monday.
$ Nana has 1 kitty.
$ Coffee has 2 kitty.
$ Kiwi has 1 kitty.
$ Coffee\'s first kitty is named "Kiffee".
```

## Local (Nested/Inner) Functions

**Local functions** are private methods of a type that are nested in another member.

```csharp
public Cat ProduceKittyWith(Cat partner)
{
    // This is a local function
    bool testIfInLove(Cat partner)
    {
        return true;
    }

    // Test if the cat is in love with the partner.
    testIfInLove( partner);

    return ProduceKitty(this, partner);
}
```

---
# Splitting Files to Organize Them [Doc](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet-new)
```bash
// Create a new project named MyBusiness
CRC_CSD-05> dotnet new console --use-program-main --name MyBusiness
// Set up a class library called PetLibrary
CRC_CSD-05> $ dotnet new classlib --name PetLibrary
// Change the folder to PetLibrary
CRC_CSD-05> $ cd PetLibrary
// Change the file name and add content to Class Cat
CRC_CSD-05/PetLibrary> $ mv Class1.cs Cat.cs
// Go back to the folder MyBusiness and run the program
CRC_CSD-05/PetLibrary> $ cd ../MyBusiness
CRC_CSD-05/MyBusiness> $ dotnet run
```

In MyBusiness.csproj, you see the configuration of the program
```csharp
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net8.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
  </PropertyGroup>

<!-- Set environment variable -->
  <ItemGroup>
    <ProjectReference
      Include="../PetLibrary/PetLibrary.csproj" />
      <!-- The slash and backslash presentation used to describe a path were not
      standardized. It causes a lot of pain.
      Some morden editors automatically convert them. -->
  </ItemGroup>

</Project>
```

In MyBusiness/Program.cs,
```csharp
using System;
using PetLibrary;

// namespace
namespace MyBusiness
{
    // Main program
    public class Program
    {
        static void Main(string[] args)
        {
            // Create a cat
            Cat nana = new Cat("Nana", new DateTime(2019, 12, 9));
            nana.WriteToConsole();

            OwnPets myPets = new OwnPets();
            myPets.WriteToConsole();
        }
    }
}
```

In PetLibrary/Cat.cs,
```csharp
// The same as namespace PetLibrary{}. We use ";" just to save indent spac
namespace PetLibrary;

public class Cat
{
    /*
    Class field, including different variables
    they can be organized by similar characteristics
    */

    // The name of the cat
    public string Name;
    // The birthday of the cat
    public DateTime DateOfBirth;
    // The children of the cat
    public List<Cat> Children = new List<Cat>();

    /*
    Class methods, where functions should be implemented
    */

    // Constructors
    // Default constructor. It will be called by default
    public Cat()
    {
        Name = "UnknownCat";
        DateOfBirth = DateTime.Today;
    }
    // Parameterized Constructor
    public Cat(string name, DateTime dateOfBirth)
    {
        this.Name = name;
        this.DateOfBirth = dateOfBirth;
    }
    // Finalizer
    ~Cat()
    {
    }

    // Print out method
    public void WriteToConsole()
    {
        Console.WriteLine($"{Name} was born on a {DateOfBirth:dddd}.");
    }

    // Static method to "multiply"
    public static Cat ProduceKitty(Cat cat1, Cat cat2)
    {
        Cat kitty = new Cat
        {
            Name = $"Baby of {cat1.Name} and {cat2.Name}"
        };
        cat1.Children.Add(kitty);
        cat2.Children.Add(kitty);
        return kitty;
    }

    // Use operators instead of the above method
    // This is called operator overloading, allowing us to redefine 
    // an existing operator
    public static Cat operator *(Cat cat1, Cat cat2)
    {
        return Cat.ProduceKitty(cat1, cat2);
    }

    // Instance method to "multiply"
    public Cat ProduceKittyWith(Cat partner)
    {
        return ProduceKitty(this, partner);
    }
}
```

In PetLibrary/Dog.cs,
```csharp
namespace PetLibrary;

// Access modifier internal can be only used inside the project
internal class Dog
{
    // Fields
    // The name of the cat
    public string Name;

    // Constructors
    // Default constructor. It will be called by default
    public Dog()
    {
        Name = "UnknownDog";
    }
}
```

In PetLibrary/OwnPets.cs,
```csharp
namespace PetLibrary;

public class OwnPets
{
    // Fields
    Cat houseCat;
    Dog houseDog;

    // Constructors
    public OwnPets()
    {
        houseCat = new Cat();
        houseDog = new Dog();
    }

    // Finalizers

    // Methods
    // Print out method
    public void WriteToConsole()
    {
        Console.WriteLine($"{houseCat}'s name is  {houseCat.Name}.");
        Console.WriteLine($"{houseDog}'s name is  {houseDog.Name}.");
    }
}
```


---
# Inheriting Classes
In C#, classes are used to create custom types. Inheritance is the process by which one class inherits the members of another class.

# Self-Defined Interface [Doc](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/interface)
An **interface** defines a contract. Any class or struct that implements that contract must provide an implementation of the members defined in the interface. Note that you cannot apply access modifiers to interface members.

The basic difference is that a **class** has both a definition and an implementation whereas an **interface** only has a definition.

**Interfaces** don't contain fields because fields represent a specific implementation of data representation, and exposing them would break encapsulation.

In MyBusiness/Program.cs,
```csharp
using System;
using Animals;

// namespace
namespace MyBusiness
{
    // Main program
    internal class Program
    {
        static void Main(string[] args)
        {
            // Create a cat
            Cat nana = new Cat("Nana", new DateTime(2019, 12, 9));

            nana.Speed = 10;
            double speed = nana.SpeedUp(2);
            Console.WriteLine($"{nana.Name} is running at speed {speed} km/hr."); 
        }
    }
}
```
In PetLibrary/Animals.cs,
```csharp
/*
The animal namespace
*/
namespace Animals
{
    public class Cat : IRun
    // ":" operator allows Cat class to reuse what has been defined in IRun.
    // Naming convention: add I for an interface name.
    {
        /*
        Class field, including different variables
        they can be organized by similar characteristics
        */

        // The name of the cat
        public string Name;
        // The birthday of the cat
        public DateTime DateOfBirth;

        /*
        Class methods, where functions should be implemented
        */

        // Constructors
        // Default constructor. It will be called by default
        public Cat()
        {
            Speed = 0.0;
            Name = "UnknownCat";
            DateOfBirth = DateTime.Today;
        }
        // Parameterized Constructor
        public Cat(string name, DateTime dateOfBirth)
        {
            Speed = 0.0;
            this.Name = name;
            this.DateOfBirth = dateOfBirth;
        }
        // Finalizer
        ~Cat()
        {
        }

        // Implementation of interface IRun
        public double Speed { get; set; }
        public int Distance { get; }
        public double SpeedUp(double velocity)
        {
            Speed += velocity;
            return Speed;
        }
    }

    // IRun is an interface
    // You have variables and methods, but you don't implement them.
    // No access modifier is allowed.
    interface IRun
    {
        // Instance field
        // double Velocity; // compile error
        // Property
        double Speed { get; set; }
        int Distance { get; }

        double SpeedUp(double velocity);
    }
}
```
```bash
$ Nana is running at speed 2 km/hr.
```

# System-Defined Interface [Doc](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/interface)

In MyBusiness/Program.cs,
```csharp
using System;
using Animals;

// namespace
namespace MyBusiness
{
    // main program
    class Program
    {
        static void Main(string[] args)
        {
            // Create a cat array
            Cat[] cats =
            {
                new Cat("Nana", new DateTime(2019, 12, 9)),
                new Cat("Coffee", new DateTime(2019, 6, 20)),
                new Cat("Kiwi", new DateTime(2018, 11, 19))
            };

            // Print the array
            foreach (Cat cat in cats)
            {
                cat.WriteToConsole();
            }

            // Sort the array
            Array.Sort(cats);

            // Print the array again
            Console.WriteLine("Use Cat's IComparable implementation to sort the cat instance:");
            foreach (Cat cat in cats)
            {
                cat.WriteToConsole();
            }
        }
    }
}
```
In PetLibrary/Animals.cs,
```csharp
/*
The animal namespace
*/
namespace Animals
{
    public class Cat : IComparable<Cat>
    // You can check the definition of IComparible
    {
        /*
        Class field, including different variables
        they can be organized by similar characteristics
        */

        // The name of the cat
        public string Name;
        // The birthday of the cat
        public DateTime DateOfBirth;

        /*
        Class methods, where functions should be implemented
        */

        // Constructors
        // Default constructor. It will be called by default
        public Cat()
        {
            Name = "UnknownCat";
            DateOfBirth = DateTime.Today;
        }
        // Parameterized Constructor
        public Cat(string name, DateTime dateOfBirth)
        {
            this.Name = name;
            this.DateOfBirth = dateOfBirth;
        }
        // Finalizer
        ~Cat()
        {
        }

        // Print out method
        public void WriteToConsole()
        {
            Console.WriteLine($"{Name} was born on a {DateOfBirth:dddd}.");
        }

        // Implementation of interface IComparible
        // Also check the class "public class Cat : IComparable<Cat>"
        public int CompareTo(Cat? anotherCat)
        {
            if (anotherCat != null)
                return Name.CompareTo(anotherCat.Name);
            else
                return 0;
        }
    }
}
```
```bash
$ Nana was born on a Monday.
$ Coffee was born on a Thursday.
$ Kiwi was born on a Monday.
$ Use Cat\'s IComparable implementation to sort the cat instance:
$ Coffee was born on a Thursday.
$ Kiwi was born on a Monday.
$ Nana was born on a Monday.
```

---
# Selected Theory

## Useful Advanced C# Data Structure

* Collections [Doc](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/collections). We will introduce one-by-one later.

## File Management

* Create and publish a package with the dotnet CLI [Doc](https://learn.microsoft.com/en-us/nuget/quickstart/create-and-publish-a-package-using-the-dotnet-cli)

* Visual Studio Code Tips and Tricks [Doc](https://code.visualstudio.com/docs/getstarted/tips-and-tricks)