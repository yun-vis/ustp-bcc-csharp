---
# permalink: /about/
layout: single
title: "Assignment"
classes: wide
header:
  image: /assets/images/teaser/teaser.png
  caption: "Image credit: [**Yun**](http://yun-vis.net)"  
last_modified_at: 2022-03-13
---

# C# Homework Assignment 1: Environement Setup
Please refer to the [setup page](https://csharp-cheatsheet.github.io/).

# ASCII Art [Doc]()

**ASCII Code:** It stands for American Standard Code for Information Interchange. [Doc](https://en.wikipedia.org/wiki/ASCII)

**ASCII Art:** ASCII art is a graphic design technique that uses computers for presentation and consists of pictures pieced together from the 95 printable (from a total of 128) characters defined by the ASCII Standard. [Examples](https://ascii.co.uk/art).
```csharp
using System;

// namespace
namespace MyApplication
{
    class TowersOfHanoiApp
    {
        public static void Main(string[] args)
        {
            int num = 5;
            for (int i = 0; i < num; i++)
            {
                string s = "";
                for (int j = 0; j < num; j++)
                {
                    if (j > num-i-2)
                        s += "*";
                    else
                        s += " ";
                }
                for (int j = 0; j < num; j++)
                {
                    if (j > i)
                        s += " ";
                    else
                        s += "*";
                }
                Console.WriteLine(s);
            }
        }
    }
}
```
```bash
$     **    
$    ****   
$   ******  
$  ********
$ **********
```

# C# Homework Assignment 2: Tower of Hanoi

```csharp
/*
The Tower Of Hanoi
*/
using System;

// namespace
namespace MyApplication
{
    class TowersOfHanoiApp
    {
        public static void Main(string[] args)
        {
            Console.WriteLine("Enter the number of discs: ");
            int discNum = Convert.ToInt32(Console.ReadLine());

            MoveTower(discNum, "L", "M", "R");
        }

        public static void MoveTower(int diskID, string from, string to, string third)
        {
            if (diskID > 0)
            {
                MoveTower(diskID - 1, from, third, to);
                Console.WriteLine("Move disk {0} from tower {1} to tower {2}",
                                   diskID, from, to);
                MoveTower(diskID - 1, third, to, from);
            }
        }
    }
}
```

# C# Homework Assignment 3: Bubble Sort

```csharp
/*
Sorting Algorithm
*/
using System;

// namespace
namespace MyApplication
{
    class Program
    {
        public static void Main(string[] args)
        {
            int[] intArray = new int[] { 4, 1, 3, 5, 6, 8, 2, 8, 5, 9 };
            string[] stringArray = new string[] { "Fish", "Meat", "Rice", "Potato", "Tea", "Milk", "Water", "Tomato", "Kiwi", "Coffee", };

            // Sort the int array
            // Before sorting
            Console.WriteLine("\nOld intArray:");
            for (int i = 0; i < intArray.Length; i++)
            {
                Console.WriteLine(intArray[i]);
            }

            BubbleSort<int> intSorter = new BubbleSort<int>();
            int[] intResult = intSorter.BubbleSorting(intArray);

            // After sorting
            Console.WriteLine("\nNew intArray:");
            for (int i = 0; i < intArray.Length; i++)
            {
                Console.WriteLine(intResult[i]);
            }

            // Sort the string array
            // Before sorting
            Console.WriteLine("\nOld stringArray:");
            for (int i = 0; i < stringArray.Length; i++)
            {
                Console.WriteLine(stringArray[i]);
            }

            BubbleSort<string> stringSorter = new BubbleSort<string>();
            string[] stringResult = stringSorter.BubbleSorting(stringArray);

            // After sorting
            Console.WriteLine("\nNew stringArray:");
            for (int i = 0; i < stringArray.Length; i++)
            {
                Console.WriteLine(stringResult[i]);
            }
        }
    }

    class BubbleSort<T> where T : IComparable<T>
    {
        public T[] BubbleSorting(T[] array)
        {
            int length = array.Length;
            for (int i = 0; i < length - 1; i++)
            {
                for (int j = 1; j < length; j++)
                {
                    // The two elements of the exchange
                    if (array[j].CompareTo(array[j - 1]) < 0)
                    {
                        T temp = array[j];
                        array[j] = array[j - 1];
                        array[j - 1] = temp;
                    }
                }
            }

            return array;
        }
    }
}
```
