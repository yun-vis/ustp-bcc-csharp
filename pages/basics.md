---
# permalink: /about/
layout: single
title: "C# Basics"
classes: wide
header:
  image: /assets/images/teaser/teaser.png
  caption: "Image credit: [**Yun**](http://yun-vis.net)"
last_modified_at: 2023-03-05
---

C# is a general-purpose, type-safe, object-oriented programming language. Now it is also open source.

# C# Basic Syntax (PART I)

## Hello, world! Example

### Console.WriteLine()
The Console.WriteLine() method is used to print text to the console.

```csharp
Console.WriteLine("Hello, world!");

string myName = "Yun";
Console.WriteLine($"Hello, world! {myName}!");  // {} allows you to
                                                // add variable in the string.
```

### Console.ReadLine()
The Console.ReadLine() method is used to get user input.
```csharp
Console.WriteLine("Enter your name: ");
string? name = Console.ReadLine();  // The ? symbol makes the name variable nullable
```

## Data Types and Variables
C# is a type-safe language. When variables are declared it is necessary to define their data type.
Types are categorized as **Value** or **Reference** by definition, but not its usage.

### int (integer)
```csharp
int a = 5;
```

### bool (boolean)
```csharp
bool b = true;
```

### string (text)
```csharp
string myName = "FirstName FamilyName";
```

### float, double, and decimal (real number)
The type of a real literal is determined by its suffix: The literal without suffix or with the d or D suffix is of type double. The literal with the f or F suffix is of type float. The literal with the m or M suffix is of type decimal.
```csharp
Console.WriteLine("Using doubles:");
double a = 0.1;
double b = 0.2;
if (a + b == 0.3)
{
    Console.WriteLine($"{a} + {b} equals to 0.3");
}
else
{
    Console.WriteLine($"{a} + {b} does NOT equal to 0.3");
}
```
What is the difference between these two code pieces?
```csharp
Console.WriteLine("Using decimals:");
decimal c = 0.1M; // M suffix means a decimal literal value
decimal d = 0.2M;
if (c + d == 0.3M)
{
    Console.WriteLine($"{c} + {d} equals to 0.3");
}
else
{
    Console.WriteLine($"{c} + {d} does NOT equal to 0.3");
}
```

### Using array to Store Multiple Variables

```csharp
// Declare an integer array of length 3 without setting the values.
int[] integers = new int[3];

// `numbers` array that stores 3 integers
int[] numbers = { 3, 14, 59 };

// 'characters' array that stores 3 strings
string[] characters = new string[] { "Nana", "Coffee", "Kiwi" };

// 2D array
int[,] twoDArray = new int[4, 2];
```

### var
```csharp
var a = 1+2;
var subTotal = 0.2;
var salesTax = 0.1;
var totalPrice = subTotal + salesTax;   // ambigious, can be float, double, or decimal, so which one is it here?
                                        // based on the types of subTotal and  salesTax.

if (totalPrice == 0.3)
{
    Console.WriteLine($"{subTotal}+{salesTax} equal to 0.3.");
}
else
{
    Console.WriteLine($"{subTotal}+{salesTax} does NOT equal to " + (subTotal + salesTax));
    Console.WriteLine($"{subTotal}+{salesTax} does NOT equal to 0.3.");
}

```

#### Best practices for var
✅ Use var when it improves readability, especially with long type names:
```csharp
var customers = new Dictionary<int, List<string>>();
```
✅ Use var in foreach loops:
```csharp
foreach (var item in myList)
{
    Console.WriteLine(item);
}
```
❌ Avoid var for simple types (like int, string, bool):
```csharp
var age = 25;  // Bad
int age = 25;  // Better
```
❌ Avoid var when the type is not obvious:
```csharp
var result = ProcessData(); // What does this return?
```

### null value
```csharp
int myNum = 4;
int? yourNum = null;  // yourNum can be empty.
```

### enum
```csharp
// A self-defined type that contains ten cat types
enum WorldCatTypes
{
    Polydactyl,
    Snowshoe,
    Calico,
    BritishShorthair,
    Siamese,
    NorwegianForestCat,
    JapaneseBobtail,
    Persian,
    ScottishFold,
    GrayTabby
}
```

## Using Operators (Symbolic Version of Methods)

### Equality Operators
```csharp
int a = 5;
int b = 10;
Console.WriteLine(a == b);  // Return and print "false" because a is not equal to b.
```

### Arithmetic Operators
```csharp
int result = 0;   // initialization
result = 10 + 5;  // addition operator
result = 10 - 5;  // subtraction operator
result = 10 * 5;  // multiplication operator
result = 10 / 5;  // division operator
result = 10 % 5;  // modulo operator (returns the remainder)
```
### Unary Operators
```csharp
int a = 10;
a++; // a = a+1
a--; // a = a-1
++a; // What is the difference?
--a;
```

```csharp
int a = 10;
int b = 0;
b = a++; // a = a+1
Console.WriteLine(a + ", " + b); 
b = a--; // a = a-1
Console.WriteLine(a + ", " + b); 
b = ++a;
Console.WriteLine(a + ", " + b); 
b = --a;
Console.WriteLine(a + ", " + b); 
```

### Logical Operators [Doc](https://en.wikipedia.org/wiki/Truth_table)

```csharp
bool b = false || true; // true;
```

### Comparison/Relational Operators
```csharp
string f = "first";
Console.WriteLine(f == "first");

int x = 10;
Console.WriteLine(x < 15);  // Return and print "true" because 10 is less than 15.
Console.WriteLine(x < 5);   // Return and print "false" because 10 is larger than 5.
```

### Bitwise Operators [Doc](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/bitwise-and-shift-operators)

```csharp
uint a = 0b_1010_0000;  // 0b tells the compiler that a is a binary literal
uint b = 0b_1001_0001;  // _ is used as a digit separator.
                        // 0b_1010_0000 is equal to 0b10100000, just easier to read.
uint c = a | b;
Console.WriteLine(Convert.ToString(c, toBase: 2));
// Output:
// 10110001
```

## Conditional Control (Selection)

### if Statements / if and else / if and ilse if

```csharp
int num = 10;

// if statement
if (num == 10)
{
    Console.WriteLine("Yes, the num is 10.");
}

// if and else statement
if (num == 10)
{
    Console.WriteLine("Yes, the num is 10.");
}
else
{
    Console.WriteLine("No, the num is not 10.");
}

// if and else if statement
if (num == 10)
{
    Console.WriteLine("Yes, the num is 10.");
}
else if (num == 20)
{
    Console.WriteLine("Yes, the num is 20.");
}
else
{
    Console.WriteLine("No, the num is neither 10 nor 20.");
}
```

### switch

```csharp
int num = 2;

void DisplayNum(double num)
{
    switch (num)
    {
        case 1:
            Console.WriteLine("1");
            break;
        case 2:
            Console.WriteLine("2");
            break;
        case 3:
        case 4:
            Console.WriteLine("3 or 4");
            break;
        case 5:
            goto case 1;  // jump, usually not preferred
        default:  // Usually for debug purpose.
            Console.WriteLine($"The num is {num}.");
            break;
    }
}
```

## Conditional Control (Repetition/Iteration)

### while

```csharp
while (x > 5)
{
  // Do something here.
}
```

### do

```csharp
do
{
    // Do something here at least once.
} while (x > 5);
```

### for

```csharp
// for( initializer; condition; iterator )
for(int i = 0; i < 10; i++)
{
    // Do something here.
    Console.WriteLine(i);
}

int[] numbers = { 3, 14, 59 };
for(int i = 0; i < numbers.Length; i++)
{
    // Do something here.
    Console.WriteLine(numbers[i]);
}
```

### foreach
```csharp
var fibNumbers = new List<int> { 0, 1, 1, 2, 3, 5, 8, 13 };
foreach (int element in fibNumbers)
{
    Console.Write($"{element} ");
}
// Output:
// 0 1 1 2 3 5 8 13
```

## Main args()
```csharp
//Simple calculator showing the use of args(), switch, and loops
using System;

class Program
{
    static void Main(string[] args)
    {
        if (args.Length < 2)
        {
            Console.WriteLine("Usage: dotnet run -[operation] numbers...");
            Console.WriteLine("Operations:");
            Console.WriteLine("  -mul x y z...    (Multiply numbers)");
            Console.WriteLine("  -sum x y z...    (Add numbers)");
            Console.WriteLine("  -div x y         (Divide x by y)");
            Console.WriteLine("  -sub x y         (Subtract y from x)");
            return;
        }

        string operation = args[0];
        double[] numbers = new double[args.Length - 1];

        // Convert input strings to numbers manually
        for (int i = 1; i < args.Length; i++)
        {
            if (!double.TryParse(args[i], out numbers[i - 1]))
            {
                Console.WriteLine($"Error: '{args[i]}' is not a valid number.");
                return;
            }
        }

        double result = 0;

        switch (operation)
        {
            case "-mul":
                result = 1; // Start with 1 for multiplication
                for (int i = 0; i < numbers.Length; i++)
                {
                    result *= numbers[i];
                }
                Console.WriteLine($"Result: {result}");
                break;

            case "-sum":
                result = 0; // Start with 0 for addition
                for (int i = 0; i < numbers.Length; i++)
                {
                    result += numbers[i];
                }
                Console.WriteLine($"Result: {result}");
                break;

            case "-div":
                if (numbers.Length != 2)
                {
                    Console.WriteLine("Error: Division requires exactly two numbers.");
                    return;
                }
                if (numbers[1] == 0)
                {
                    Console.WriteLine("Error: Division by zero is not allowed.");
                    return;
                }
                result = numbers[0] / numbers[1];
                Console.WriteLine($"Result: {result}");
                break;

            case "-sub":
                if (numbers.Length != 2)
                {
                    Console.WriteLine("Error: Subtraction requires exactly two numbers.");
                    return;
                }
                result = numbers[0] - numbers[1];
                Console.WriteLine($"Result: {result}");
                break;

            default:
                Console.WriteLine("Error: Unknown operation. Use -mul, -sum, -div, or -sub.");
                break;
        }
    }
}
```

### C# Jump Statements [Doc](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/statements/jump-statements)


### Collatz Conjecture as an example

```csharp
using System;

namespace CollatzConjecture
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Please input a positive number:");

            int? num = Int32.Parse(Console.ReadLine());

            if (num == null || num <= 0)
            {
                Console.WriteLine("Sorry, the number should be larger than 1!");
                return;
            }

            int steps = 0;
            while (num != 1)
            {
                steps += 1;
                if (num % 2 == 0)
                {
                    num = num / 2;
                }
                else
                {
                    num = num * 3 + 1;
                }
            }

            if (num == 1)
            {
                Console.WriteLine($"Oh yeah, we reach 1 with {steps} steps!");
            }
        }
    }
}
```


# C# Basic Syntax (PART II)


## Using Methods

A method is a code block that contains a series of statements.

In C#, a method declaration includes
OptionalModifier ReturnType TheMethodName( ParameterType parameterName )
Also note that **return** only takes one parameter.

### Variables Inside Methods (The Scope of Methods)

Parameters and variables declared inside of a method can be only used under the scope of the method.
Return type should be matched.
A method can have optional parameters

```csharp
using System;

namespace CRC_CSD_03; // File scoped namespaces

class Program
{
    static void Main(string[] args)
    {
        // Any of the following are valid method calls.
        AddSomeNumbers(1);          // Returns 6.
        AddSomeNumbers(1, 1);       // Returns 4.
        AddSomeNumbers(3, 3, 3);    // Returns 9.

        int value = 0;
        if (args.Length == 0)
        {
            Console.WriteLine($"The value is {value}.");
        }
        else if (args.Length == 1)
        { 
            // int.Parse is a system method: Convert string to int
            value = AddSomeNumbers(int.Parse(args[0]));
            Console.WriteLine($"The value is {value}.");
        }
        else if (args.Length == 2)
        { 
            value = AddSomeNumbers(int.Parse(args[0]), int.Parse(args[1]));
            Console.WriteLine($"The value is {value}.");
        }
        else
        { 
            value = AddSomeNumbers(int.Parse(args[0]), int.Parse(args[1]), int.Parse(args[2]));
            Console.WriteLine($"The value is {value}.");
        }

        // a = 10; // compile error! The scope for a is not correct!
        PrintMyName("Yun");
    }

    /*
    Main: The class of my main program, where the application begins.
    Input:
        x: int
        y: int, optional
        z: int, optional
    Output:
        int
    */
    static int AddSomeNumbers(int x, int y = 3, int z = 2)
    {
        int a = 5;

        // return int
        return x + y + z + a;
    }

    // return void, nothing to return
    static void PrintMyName(string myName)
    {
        Console.WriteLine($"My name is {myName}.");
    }
}
```

### System Methods

Math.Sqrt() is a Math class method to calculate the square root of a value. "." operator allows us to access a method of a class.
```csharp
Console.WriteLine(Math.Sqrt(9));
```
```bash
$ 3
```


### Call by Value vs. Call by Reference
Passing parameters in a method can be done by deep copying or referencing.

```csharp
using System;

namespace CRC_CSD_03
{
    class Program
    {
        static void Main(string[] args)
        {
            int number = 4;
            SquareVal(number);
            Console.WriteLine(number);
            // Output: 4

            SquareRef(ref number);
            Console.WriteLine(number);
            // Output: 16
        }

        /*
        SquareVal: square a number.
        Input:
          num: int
        Output:
          none
        */
        static void SquareVal(int num)
        {
            num *= num; // num = num * num
        }

        /*
        SquareVal: square a number.
        Input:
          num: ref int
        Output:
          none
        */
        static void SquareRef(ref int num)
        {
            num *= num; // num = num * num
        }
    }
}
```
```bash
$ 4
$ 16
```

---
# Selected Theory

## Recursion vs. Iteration

Factorial of a Given Number can be implemented using **Recursion** or **Iteration**.

```csharp
using System;

namespace CRC_CSD_03
{
    class Program
    {
        static void Main(string[] args)
        {
            int num = 5;
            Console.WriteLine("Factorial of " + num +
                              " using Recursion is: " +
                              FactorialUsingRecursion(num));

            Console.WriteLine("Factorial of " + num +
                              " using Iteration is: " +
                              FactorialUsingIteration(num));
        }

        /*
        FactorialUsingRecursion: find factorial of given number using recurrsion.
        Input:
          num: int
        Output:
          int
        */
        static int FactorialUsingRecursion(int n)
        {
            if (n == 1)
                return 1;

            // recursion call
            return n * FactorialUsingRecursion(n - 1);
        }

        /*
        FactorialUsingIteration: find factorial of given number using iteration.
        Input:
          num: int
        Output:
          int
        */
        static int FactorialUsingIteration(int n)
        {
            int res = 1;

            // using iteration
            for (int i = 2; i <= n; i++) 
            {
                res *= i;
            }

            return res;
        }
    }
}
```
```bash
$ Factorial of 5 using Recursion is: 120
$ Factorial of 5 using Iteration is: 120
```


Fibonacci Sequence can be implemented using **Recursion** or **Iteration**.

```csharp
using System;

namespace CRC_CSD_03
{
    class Program
    {
        static void Main(string[] args)
        {
            // initialization
            int num = 5;
            int[] sequence = new int[num];

            // Calculate and print out the Fibonacci Sequence
            // Recurrsion
            resetFibonacciSequence(sequence);
            Console.Write("A Fibonacci Sequence of elements " + num +
                              " using Recursion is: ");
            FibonacciUsingRecursion(num, sequence);
            printFibonacciSequence(sequence);

            // Iteration
            resetFibonacciSequence(sequence);
            Console.Write("A Fibonacci Sequence of elements " + num +
                              " using Iteration is: ");
            FibonacciUsingIteration(num, sequence);
            printFibonacciSequence(sequence);
        }

        /*
        resetFibonacciSequence: reset the sequence
        Input:
          sequence: int[]
        Output:
          none
        */
        static void resetFibonacciSequence(int[] sequence)
        {
            for (int i = 0; i < sequence.Length; i++)
            {
                sequence[i] = -1;
            }
        }

        /*
        printFibonacciSequence: print the sequence
        Input:
          sequence: int[]
        Output:
          none
        */
        static void printFibonacciSequence(int[] sequence)
        {
            for (int i = 0; i < sequence.Length; i++)
            {
                Console.Write(sequence[i] + " ");
            }
            Console.WriteLine("");
        }

        /*
        FibonacciUsingRecursion: find the Fibonacci sequence of a given element 
        number using recurrsion.
        Input:
          num: int
          sequence: int[]
        Output:
          int
        */
        static int FibonacciUsingRecursion(int num, int[] sequence)
        {
            if (num == 1)
            {
                sequence[0] = 0;
                return 0;
            }
            else if (num == 2)
            {
                sequence[0] = 0;
                sequence[1] = 1;
                return 1;
            }
            else
            {
                // recursion call
                int value = FibonacciUsingRecursion(num - 2, sequence) 
                            + FibonacciUsingRecursion(num - 1, sequence);
                sequence[num - 1] = value;
                return value;
            }
        }

        /*
        FibonacciUsingIteration: find the Fibonacci sequence of a given element 
        number using iteration.
        Input:
          num: int
          sequence: int[]
        Output:
          none
        */
        static void FibonacciUsingIteration(int num, int[] sequence)
        {
            if (num == 1)
            {
                sequence[0] = 0;
                return;
            }
            else if (num == 2)
            {
                sequence[0] = 0;
                sequence[1] = 1;
                return;
            }
            else
            {
                sequence[0] = 0;
                sequence[1] = 1;
                // using iteration
                for (int i = 2; i < num; i++)
                {
                    sequence[i] = sequence[i - 2] + sequence[i - 1];
                }
            }
        }
    }
}
```
```bash
$ A Fibonacci Sequence of elements 5 using Recursion is: 0 1 1 2 3
$ A Fibonacci Sequence of elements 5 using Iteration is: 0 1 1 2 3
```


---
# External Resources

* [File Scoped Namespaces](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-10.0/file-scoped-namespaces)
