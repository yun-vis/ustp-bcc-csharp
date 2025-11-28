---
# permalink: /about/
layout: single
title: ".Net Type"
classes: wide
header:
  image: /assets/images/teaser/teaser.png
  caption: "Image credit: [**Yun**](http://yun-vis.net)"  
last_modified_at: 2025-02-06
---

# How to improve code readability?

## Syntactic sugar

Syntactic sugar is syntax within a programming language that is designed to make things easier to read or to express.

# Operator, Expression, and Statement

```csharp
int num = 2*3;
```

## [Operator](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/#see-also)
C# provides a number of operators. Many of them are supported by the built-in types and allow you to perform basic operations with values of those types

## [Expression](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators)
The simplest C# expressions are literals (for example, integer and real numbers) and names of variables. You can combine them into complex expressions by using operators. Operator precedence and associativity determine the order in which the operations in an expression are performed. You can use parentheses to change the order of evaluation imposed by operator precedence and associativity.

## [Statement](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/statements)
The actions that a program takes are expressed in statements. Common actions include declaring variables, assigning values, calling methods, looping through collections, and branching to one or another block of code, depending on a given condition.


# Lambda Expression and Anonymous Functions [Doc](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-expressions)

You use a lambda expression to create an anonymous function. Use the lambda declaration operator **=>** to separate the lambda's parameter list from its body. A lambda expression can be of any of the following two forms:

* **Expression lambda** that has an expression as its body:

```csharp
(input-parameters) => expression
```

* **Statement lambda** that has a statement block as its body:

```csharp
(input-parameters) => { <sequence-of-statements> }
```

```csharp
// Lambda Expression
using System;

namespace MyBusiness
{
    class Program
    {
        static void Main(string[] args)
        {
            // Local function
            bool compareMethod(int a, int b)
            {
                return a == b;
            }
            Console.WriteLine(compareMethod(3, 4));
            
            // Expression lambda
            bool compareLambda(int a, int b) => (a == b);
            Console.WriteLine(compareLambda(3, 4));

            // Print a Fibonacci sequence
            for (int i = 0; i < 10; i++)
            {
                Console.WriteLine("The {0} term of the Fibonacci sequence is {1:N0}.",
                  arg0: i + 1,
                //   arg1: FibMethod(term: i));
                  arg1: FibLambda(term: i)); 
                // N0: The numeric ("N") format specifier converts a number to a string of the form. N0 does not represent any decimal place but rounding is applied to it.
            }
        }

        // Fibonacci sequence
        static int FibMethod(int term)
        {
            switch (term)
            {
                case 0:
                    return 0;
                case 1:
                    return 1;
                default:
                    return FibMethod(term - 1) + FibMethod(term - 2);
            }
        }

        // Fibonacci sequence
        // Statement lambda
        static int FibLambda(int term) => term switch
        {
            0 => 0,
            1 => 1,
            _ => FibLambda(term - 1) + FibLambda(term - 2)
        };
    }
}
```


# Delegates [Doc](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/delegates/)

## Basic Delegates

A delegate is a type that represents references to methods with a particular parameter list and return type. When you instantiate a delegate, you can associate its instance with any method with a compatible signature (the method name, and the type and order of parameters) and return type. You can invoke (or call) the method through the delegate instance.

```csharp
using System;

namespace MyBusiness
{
    class Program
    {
        // Delegate declaration
        public delegate int[] GenerateMyNumbers(int x, int y);

        static void Main(string[] args)
        {
            // Create delegate objects/instances, where you put the corresponding methods as input parameters.
            GenerateMyNumbers generateRandom = new GenerateMyNumbers(GetRandomNumber);
            GenerateMyNumbers generateOrdered = new GenerateMyNumbers(GetOrderedNumber);

            // int[] numbers = generateRandom(10, 3);
            int[] numbers = generateOrdered(10, 3);

            foreach (int n in numbers)
            {
                Console.Write(n + " ");
            }
            Console.WriteLine();
        }

        // Create an array with size amount and assign a random value 0-maxNum in this array
        public static int[] GetRandomNumber(int maxNum, int amount)
        {
            Random random = new Random();
            int[] nums = new int[amount];

            for (int i = 0; i < amount; i++)
            {
                // 0 ~ maxNum-1
                nums[i] = random.Next(0, maxNum);
            }
            return nums;
        }

        // Get an ordered integer sequence from min to max
        public static int[] GetOrderedNumber(int max, int min)
        {
            // Avoid when max is smaller than min
            if (max < min)
            {
                int[] noNum = { 0 };
                return noNum;
            }

            // Create an ordered sequence
            int[] nums = new int[max - min + 1];
            for (int i = 0; i <= max - min; i++)
            {
                nums[i] = min + i;
            }
            return nums;
        }
    }
}
```
```bash
$ 3 4 5 6 7 8 9 10
```

* Delegates are used to pass methods as arguments to other methods.
* Delegates can be used to define callback methods.
* Delegates can be chained together; for example, multiple methods can be called on a single event.
* Lambda expressions (in certain contexts) are compiled to delegate types.

```csharp
using System;

namespace MyBusiness
{
    class Program
    {
        static void Main(string[] args)
        {
            int[] array = new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9 };

            // string.Join: method that lets you concatenate each element in an
            // object array without explicitly converting its elements to strings
            Console.WriteLine(string.Join(",", AddOne(array)));
            Console.WriteLine(string.Join(",", MultiplyTwo(array)));
            Console.WriteLine(string.Join(",", Square(array)));
        }

        // Take out each element in an array and +1
        public static int[] AddOne(int[] _array)
        {
            int[] array = new int[_array.Length];
            for (int i = 0, c = _array.Length; i < c; i++)
            {
                array[i] = _array[i] + 1;
            }
            return array;
        }

        // Take out each element in an array and *2
        public static int[] MultiplyTwo(int[] _array)
        {
            int[] array = new int[_array.Length];
            for (int i = 0, c = _array.Length; i < c; i++)
            {
                array[i] = _array[i] * 2;
            }
            return array;
        }

        // Take out each element in an array and square it
        public static int[] Square(int[] _array)
        {
            int[] array = new int[_array.Length];
            for (int i = 0, c = _array.Length; i < c; i++)
            {
                array[i] = _array[i] * _array[i];
            }
            return array;
        }
    }
}
```
```bash
$ 2,3,4,5,6,7,8,9,10
$ 2,4,6,8,10,12,14,16,18
$ 1,4,9,16,25,36,49,64,81
```

```csharp
using System;

namespace MyBusiness
{
    class Program
    {
        // Declaration of the delegete
        public delegate int ChangeValueDelegate(int x);

        static void Main(string[] args)
        {
            int[] array = new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9 };

            // Create three delegate objects that take differentmethods as parameters
            ChangeValueDelegate myDelegate1 = new ChangeValueDelegate(AddOne);
            ChangeValueDelegate myDelegate2 = new ChangeValueDelegate(MultiplyTwo);
            ChangeValueDelegate myDelegate3 = new ChangeValueDelegate(Square);
            // The following is also a valid syntax;
            // ChangeValueDelegate myDelegate3 = Square;

            // string.Join: method that lets you concatenate each element in an
            // object array without explicitly converting its elements to strings
            Console.WriteLine(string.Join(",", Change(array, myDelegate1)));
            Console.WriteLine(string.Join(",", Change(array, myDelegate2)));
            Console.WriteLine(string.Join(",", Change(array, myDelegate3)));
        }

        public static int AddOne(int number)
        {
            return number + 1;
        }
        public static int MultiplyTwo(int number)
        {
            return number * 2;
        }
        public static int Square(int number)
        {
            return number * number;
        }
        // The following is also a valid syntax using lambda expression
        // public static int Square(int number) => number * number;

        // A method Change that takes another method as the input parameters
        // In this case, the method (as a parameter) should be defined as a delegate
        public static int[] Change(int[] _array, ChangeValueDelegate changeValue)
        {
            int[] array = new int[_array.Length];
            for (int i = 0, c = _array.Length; i < c; i++)
            {
                array[i] = changeValue(_array[i]);
            }
            return array;
        }
    }
}
```
```bash
$ 2,3,4,5,6,7,8,9,10
$ 2,4,6,8,10,12,14,16,18
$ 1,4,9,16,25,36,49,64,81
```

## Lambda Expression with Delegates

```csharp
public static int Square(int number) => number * number;
```

## [Generic Delegates](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/generic-delegates)

```csharp
public delegate T ChangeValueDelegate<T>(T x);
```

## Action, Func, and Predicate Delegates

* **Action Delegate:** Encapsulates a method that does not return a value. [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.action-1?view=net-6.0)

```csharp
using System;

namespace MyBusiness
{
    class Program
    {
        static void Main(string[] args)
        {
            Action<int, int> Addition = new Action<int, int>(AddNumbers);
            // Alternative
            // Action<int, int> Addition = AddNumbers;  
            Addition(10, 20);
        }

        // add param1 and param2 and return the sum
        private static void AddNumbers(int param1, int param2)
        {
            int result = param1 + param2;
            Console.WriteLine($"Addition result = {result}");
        }
    }
}
```
```bash
$ Addition result = 30
```

* **Func<T,TResult> Delegate:** Encapsulates a method that has parameters (up to 16) and returns a value of the type specified by the TResult parameter. [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.func-2?view=net-6.0)[Example](https://learn.microsoft.com/en-us/dotnet/api/system.func-1?view=net-6.0)

```csharp
using System;

namespace MyBusiness
{
    class Program
    {
        static void Main(string[] args)
        {
            // Declare a Func delegate
            Func<int, int, int> Addition = new Func<int, int, int>(AddNumbers);
            // Func<int, int, int> Addition = AddNumbers;
            // Using Lambda Expression
            // Func<int, int, int> Addition = (param1, param2) => param1 + param2;  

            int result = Addition(10, 20);
            Console.WriteLine($"Addition result = {result}");
        }

        // add param1 and param2 and return the sum
        private static int AddNumbers(int param1, int param2)
        {
            return param1 + param2;
        }
    }
}
```
```bash
$ Addition result = 30
```

* Advantages of Action and Func Delegates
  + Easy and quick to define delegates.
  + Makes code short.
  + Compatible type throughout the application.

* **Predicate Delegate:** Represents the method that defines a set of criteria and determines whether the specified object meets those criteria. [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.predicate-1?view=net-6.0)

Syntax difference between predicate & func is that here in predicate, you can only take one input parameter and you don't specify a return type because it is always a **bool**.

```csharp
using System;

namespace MyBusiness
{
    class Program
    {
        static void Main(string[] args)
        {
            Predicate<string> CheckIfApple = new Predicate<string>(IsApple);
            // Predicate<string> CheckIfApple = IsApple;
            bool result = IsApple("IPhone X");
            if (result){
                Console.WriteLine("It's an IPhone");
            }
        }

        private static bool IsApple(string modelName)
        {
            // Check if the model name an iPhone
            if (modelName == "IPhone X")
                return true;
            else
                return false;
        }
    }
}
```
```bash
$ It\'s an IPhone
```

## Delegate exercise: magic item damage calculator

###  Starting Code
```csharp
using System;

delegate int DamageModifier(int baseDamage);
class Program
{
    static void Main()
    {
        // Character base stats
        int strength = 10;
        int dexterity = 12;
        int intelligence = 8;

        //Randomizer
        Random rng = new();

        // Modifier dictionary: each string maps to a lambda function that modifies damage
        Dictionary<string, DamageModifier> modifiers = new Dictionary<string, DamageModifier>
        {
            ["giant"] = dmg => dmg + strength,
            ["random"] = dmg => dmg * rng.Next(0, 2)*2,
            ["brutal"] = dmg => (dmg * dmg)/5
        };

        int baseDamage = 10;
        string modifier = "giant";

        int finalDamage = modifiers[modifier](baseDamage);
        Console.WriteLine($"Final Damage with {modifier} modifier: {finalDamage}");



    }
}
```
### Final Code
```csharp
using System;

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
            totalDamage += damageModifier(this.BaseDamage);
        }

        return totalDamage / durationInSeconds;
    }
}

//Delegate used to calculate composite damage
//equivalent to Func<int,int>
delegate int DamageModifier(int baseDamage);

class Program
{
    static void Main()
    {
        // Character base stats
        int strength = 10;
        int dexterity = 12;
        int intelligence = 8;

        //Randomizer
        Random rng = new();

        //Base weapons dictionary
        var weapons = new Dictionary<string,BaseWeapon>
        {
            ["sword"] = new BaseWeapon { BaseDamage = 10, AttackSpeed = 1.0 },
            ["dagger"] = new BaseWeapon { BaseDamage = 5, AttackSpeed = 0.5 },
            ["axe"] = new BaseWeapon { BaseDamage = 20, AttackSpeed = 2.0 }
        };

        // Modifier dictionary: each string maps to a lambda function that modifies damage
        Dictionary<string, DamageModifier> modifiers = new Dictionary<string, DamageModifier>
        {
            ["giant"] = dmg => dmg + strength,
            ["random"] = dmg => dmg * rng.Next(0, 2)*2,
            ["brutal"] = dmg => (dmg * dmg)/5
        };

        // Example item with modifiers
        List<string> itemModifiers = ["giant","brutal"];
        string baseWeaponName = "dagger";

        // Compose damage function
        DamageModifier calculateDamage = dmg => dmg;
        foreach (var mod in itemModifiers)
        {
            if (modifiers.ContainsKey(mod))
            {
                DamageModifier modFunc = modifiers[mod];
                DamageModifier previousFunc = calculateDamage;

                // Compose previous with new modifier
                calculateDamage = dmg => modFunc(previousFunc(dmg));
            }
        }

        int finalDamage = calculateDamage(weapons[baseWeaponName].BaseDamage);
        string modifierLabel = string.Join(" ", itemModifiers);
        Console.WriteLine($"Final Damage for the {modifierLabel} {baseWeaponName}: {finalDamage}");
        Console.WriteLine($"DPS: {weapons[baseWeaponName].CalculateDPS(calculateDamage, 100000)}");
    }
}
```

# Type-testing Operators and Cast Expression

## [Object Class](https://learn.microsoft.com/en-us/dotnet/api/system.object?view=net-6.0)

Definition: Supports all classes in the .NET class hierarchy and provides low-level services to derived classes. This is the ultimate base class of all .NET classes; it is the root of the type hierarchy.

```csharp
object myObject1 = new Cat();
// You can use a base/parent class to refer to your object
Animal animal1 = new Dog();
object myObject2 = animal1;
```

Problem: How do we know/guarantee what information has been stored in the object?

## Implicit Casting

```csharp
// Implicit casting
Cat nana = new Cat();
WildCat leopard = new WildCat();
Cat petCat = leopard;
Console.Write($"{petCat.Name} speaks ");
petCat.Speak();
// Compile error
// WildCat wildCat = petCat; 
```

## Explicit Casting

```csharp
// Explicit casting
WildCat wildCat = (WildCat)petCat;
// Runtime error
// WildCat wildCat = (WildCat)nana;
Console.Write($"{wildCat.Name} speaks ");
wildCat.Speak();
```

```csharp
public class Cat
{
    public string Name = "ACat";
    public virtual void Speak()
    {
        Console.WriteLine("Meow!");
    }
}

public class WildCat : Cat
{
    public int Age = 0;
    public override void Speak()
    {
        Console.WriteLine("WildMeow!");
    }
}
```

You can also overload the implicit and explicit operators in C# [Doc](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/user-defined-conversion-operators).

## Avoiding Casting Exceptions

```csharp
// Use is operator
if (petCat is WildCat)
{
    Console.WriteLine($"{petCat.Name} IS an WildCat");
    WildCat wCat = (WildCat)petCat;
    // safely do something with wCat
}
```

## is Operator

The **is** operator will check if the run-time type of an expression is compatible with a given type. The **as** operator considers only reference, nullable, boxing, and unboxing conversions.

## as Operator

The **as** operator is used to explicitly convert an expression to a given type if its run-time type is compatible with that type. The as operator returns null if the conversion is not possible.

In MyBusiness/Program.cs,
```csharp
namespace MyBusiness;

class Program
{
    static void Main(string[] args)
    {
        object myObject1 = new Cat();
        // You can use a base/parent class to refer to your object 
        Animal animal1 = new Dog();
        object myObject2 = animal1;

        // Implicit casting
        Cat nana = new Cat();
        WildCat leopard = new WildCat();
        Cat petCat = leopard;
        Console.Write($"{petCat.Name} speaks ");
        petCat.Speak();
        // Compile error
        // WildCat wildCat = petCat; 

        // Explicit casting
        WildCat wildCat = (WildCat)petCat;
        // Runtime error
        // WildCat wildCat = (WildCat)nana;
        Console.Write($"{wildCat.Name} speaks ");
        wildCat.Speak();

        // Use is operator to safely check if the types are compatible
        if (petCat is WildCat)
        {
            Console.WriteLine($"{petCat.Name} IS an WildCat");
            WildCat wCat = (WildCat)petCat;
            // safely do something with wCat
        }

        // object is a base class of all derived classes in C#
        object[] myObjects = new object[4];
        myObjects[0] = new Dog();
        myObjects[1] = new Cat();
        myObjects[2] = "StringDog";
        myObjects[3] = "StringCat";

        for (int i = 0; i < myObjects.Length; i++)
        {
            // Convert an element in the myobjects array to a string element
            string? s = myObjects[i] as string;
            // Print out the current element
            Console.Write($"Inspecting element: {myObjects[i]}");

            // If converted successfully, s will be a string, otherwise return null.
            if (s == null)
            {
                Console.Write(" --> Incompatible type");
            }
            else
            {
                Console.Write(" --> Compatible type");
            }
            Console.WriteLine(", with string!");
        }
    }
}
```

In AnimalLibrary/Animals.cs,
```csharp
public class Animal
{
    public virtual void Speak()
    {
        Console.WriteLine("#$&%");
    }
}

public class Dog : Animal
{
    public override void Speak()
    {
        Console.WriteLine("Woof!");
    }
}

public class Cat : Animal
{
    public string Name = "UnknownCat";
    public override void Speak()
    {
        Console.WriteLine("Meow!");
    }
}

public class WildCat : Cat
{    
    public override void Speak()
    {
        Console.WriteLine("WildMeow!");
    }
}
```



---
# Environment.SpecialFolder Enum [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.environment.specialfolder?view=net-6.0)

# Other Interesting Types

* System.Numerics (BigInteger, Complex, Quaternion)

---
# Selected Theory

## [Standard Numeric Format Strings](https://learn.microsoft.com/en-us/dotnet/standard/base-types/standard-numeric-format-strings)
