---
# permalink: /about/
layout: single
title: "Collections"
classes: wide
header:
  image: /assets/images/teaser/teaser.png
  caption: "Image credit: [**Yun**](http://yun-vis.net)"  
last_modified_at: 2022-03-13
---

# Static and Dynamic Data Structure

## Array (Static at Runtime) / List (Dynamic at Runtime)

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
            Cat[] catArray = new Cat[3];
            List<Cat> catList = new List<Cat>();

            // Initialize an array
            catArray[0] = new Cat("Nana");
            catArray[1] = new Cat("Coffee");
            catArray[2] = new Cat("Kiwi");

            // Iterate the array to create cats
            catList.Add(new Cat("Nana"));
            catList.Add(new Cat("Coffee"));
            catList.Add(new Cat("Kiwi"));
        }
    }
}
```

```csharp
/*
The animal namespace
*/
namespace Animals
{
    public class Cat
    {
        public string Name{ get; set; }

        public Cat()
        {
            this.Name = "unknown";
        }
        public Cat( string name )
        {
            this.Name = name;
        }
    }
}
```

# Collections

If you need to store multiple values in a variable, then you can use a collection. A **collection** is a data structure in memory that can manage multiple items in different ways. In comparison to an **array**, collections enable dynamic changes.

# System.Collections.Generic Namespace [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic?view=net-6.0)

* **System.Collections:** Interfaces and base classes used by collections.
* **System.Collections.Generic:** Introduced in C# 2.0 with .NET Framework 2.0. These collections allow you to specify the type you want to store using a generic type parameter (which is safer, faster, and more efficient).
* **System.Collections.Concurrent**
* **System.Collections.Immutable**

# Common Features of All Collections

All collections implement the **ICollection** interface; this means that they must have a Count property to tell you how many objects are in them.

```csharp
int listCount = catList.Count;
Console.WriteLine($"The total elements in the list is {listCount}.");
```

All collections implement the IEnumerable interface, which means that they must have a
GetEnumerator method that returns an object that implements IEnumerator; this means that
the returned object must have a MoveNext method and a Current property so that they can be
iterated using the foreach statement.

```csharp
// The foreach statement
foreach (Cat cat in catList)
{
    // do something with each cat
    Console.WriteLine($"The name of the cat is {cat.Name}.");
}
```

## List Class [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.list-1?view=net-6.0)

Represents a strongly typed list of objects that can be accessed by index. Provides methods to search, sort, and manipulate lists. Lists are a good choice when you want to **manually** control the order of items in a collection.

Non-generic type: ArrayList [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.collections.arraylist?view=net-6.0)   

|Index   |Item    |
|--------|--------|
|0       |Austria |
|1       |Taiwan  |
|2       |Austria |
|3       |Germany |

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
            List<string> countryList = new List<string>();
            countryList.Add("Austria");
            countryList.Add("Taiwan");
            countryList.Add("Austria");
            countryList.Add("Germany");

            // Print the current list
            foreach (string item in countryList)
            {
                Console.WriteLine(item);
            }

            // Contain method
            Console.WriteLine(countryList.Contains("Taiwan"));

            // Insert method
            countryList.Insert(2, "Japan");

            // Print the current list
            foreach (string item in countryList)
            {
                Console.WriteLine(item);
            }

            // Insert method
            countryList.Remove("Japan");
            // countryList.RemoveAt(2);

            // Print the current list
            foreach (string item in countryList)
            {
                Console.WriteLine(item);
            }
        }
    }
}
```
```bash
$ Austria
$ Taiwan
$ Austria
$ Germany

$ True

$ Austria
$ Taiwan
$ Japan
$ Austria
$ Germany

$ Austria
$ Taiwan
$ Austria
$ Germany
```

## Dictionary<TKey, TValue> Class [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2?view=net-6.0)

Non-generic type: HashTable [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.collections.hashtable?view=net-6.0)   

```csharp
using System;
using System.Collections.Generic;

// namespace
namespace MyBusiness
{
    // main program
    class Program
    {
        static void Main(string[] args)
        {
            // Create a new dictionary of strings, with string keys.
            Dictionary<int, string> numberNames = new Dictionary<int, string>();

            /*
            Add
            */
            // Adding a key/value using the Add() method
            numberNames.Add(1, "One");
            numberNames.Add(2, "Two");
            numberNames.Add(3, "Three");
            // Runtime error: An item with the same key has already been added.
            // numberNames.Add(3, "Three");

            foreach (KeyValuePair<int, string> kvp in numberNames)
                Console.WriteLine("Key: {0}, Value: {1}", kvp.Key, kvp.Value);

            //creating a dictionary using collection-initializer syntax
            Dictionary<string, string> cities = new Dictionary<string, string>(){
                {"UK", "London, Manchester, Birmingham"},
                {"USA", "Chicago, New York, Washington"},
                {"India", "Mumbai, New Delhi, Pune"}
            };

            // foreach (KeyValuePair<string, string> kvp in cities)
            foreach (var kvp in cities)
            {
                Console.WriteLine("Key: {0}, Value: {1}", kvp.Key, kvp.Value);
            }

            /*
            Access elements
            */
            //prints value of UK key
            Console.WriteLine(cities["UK"]);
            // run-time exception: Key does not exist      
            // Console.WriteLine(cities["France"]);       
            //use ContainsKey() to check for an unknown key
            if (cities.ContainsKey("France"))
            {
                Console.WriteLine(cities["France"]);
            }
            else
            {
                Console.WriteLine("The key \"France\" does not exist!");
            }

            //use ElementAt() to retrieve key-value pair using index
            for (int i = 0; i < cities.Count; i++)
            {
                Console.WriteLine("Key: {0}, Value: {1}",
                                                        cities.ElementAt(i).Key,
                                                        cities.ElementAt(i).Value);
            }

            /*
            Update Dictionary
            */
            if (cities.ContainsKey("USA"))
            {
                cities["USA"] = "Seattle";
            }
            foreach (var kvp in cities)
            {
                Console.WriteLine("Key: {0}, Value: {1}", kvp.Key, kvp.Value);
            }
        }
    }
}
```
```bash
$ Key: 1, Value: One
$ Key: 2, Value: Two
$ Key: 3, Value: Three

$ Key: UK, Value: London, Manchester, Birmingham
$ Key: USA, Value: Chicago, New York, Washington
$ Key: India, Value: Mumbai, New Delhi, Pune

$ London, Manchester, Birmingham
$ The key "France" does not exist!

$ Key: UK, Value: London, Manchester, Birmingham
$ Key: USA, Value: Chicago, New York, Washington
$ Key: India, Value: Mumbai, New Delhi, Pune

$ Key: UK, Value: London, Manchester, Birmingham
$ Key: USA, Value: Seattle
$ Key: India, Value: Mumbai, New Delhi, Pune
```

## HashSet Class [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.hashset-1?view=net-6.0)


```csharp
using System;
using System.Collections.Generic;

// namespace
namespace MyBusiness
{
    // main program
    class Program
    {
        static void Main(string[] args)
        {
            // Create a new dictionary of strings, with string keys.
            HashSet<int> evenNumbers = new HashSet<int>();
            HashSet<int> oddNumbers = new HashSet<int>();

            /*
            Add
            */
            // Adding a key/value using the Add() method
            for (int i = 0; i < 5; i++)
            {
                // Populate numbers with just even numbers.
                evenNumbers.Add(i * 2);

                // Populate oddNumbers with just odd numbers.
                oddNumbers.Add((i * 2) + 1);
            }

            /*
            Count method
            */
            Console.Write("evenNumbers contains {0} elements: ", evenNumbers.Count);
            DisplaySet(evenNumbers);

            Console.Write("oddNumbers contains {0} elements: ", oddNumbers.Count);
            DisplaySet(oddNumbers);

            /*
            Set operation union
            */
            // Create a new HashSet populated with even numbers.
            HashSet<int> numbers = new HashSet<int>(evenNumbers);
            Console.WriteLine("numbers UnionWith oddNumbers...");
            numbers.UnionWith(oddNumbers);
            // numbers.IntersectWith(oddNumbers);

            Console.Write("numbers contains {0} elements: ", numbers.Count);
            DisplaySet(numbers);

            // Local function
            void DisplaySet(HashSet<int> collection)
            {
                Console.Write("{");
                foreach (int i in collection)
                {
                    Console.Write(" {0}", i);
                }
                Console.WriteLine(" }");
            }
        }
    }
}
```
```bash
$ evenNumbers contains 5 elements: { 0 2 4 6 8 }
$ oddNumbers contains 5 elements: { 1 3 5 7 9 }
$ numbers UnionWith oddNumbers...
$ numbers contains 10 elements: { 0 2 4 6 8 1 3 5 7 9 }
```

## SortedList<TKey,TValue> Class [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.sortedlist-2?view=net-6.0)

```csharp
using System;
using System.Collections.Generic;

// namespace
namespace MyBusiness
{
    // main program
    class Program
    {
        static void Main(string[] args)
        {
            //SortedList of int keys, string values
            SortedList<int, string> numberNames = new SortedList<int, string>();

            //using collection-initializer syntax
            // SortedList<int, string> numberNames = new SortedList<int, string>()
            //                 {
            //                     {3, "Three"},
            //                     {1, "One"},
            //                     {2, "Two"},
            //                 };

            /*
            Add
            */
            numberNames.Add(3, "Three");
            numberNames.Add(1, "One");
            numberNames.Add(2, "Two");
            numberNames.Add(4, null);
            numberNames.Add(10, "Ten");
            numberNames.Add(5, "Five");

            //The following will throw exceptions
            //Compile-time error: key must be int type
            // numberNames.Add("Three", 3);
            //Run-time exception: duplicate key
            // numberNames.Add(1, "One");
            //Run-time exception: key cannot be null
            // numberNames.Add(null, "Five");

            /*
            Access
            */
            foreach (KeyValuePair<int, string> kvp in numberNames)
            {
                Console.WriteLine("key: {0}, value: {1}", kvp.Key, kvp.Value);
            }
            Console.WriteLine(numberNames[2]);
            // for (int i = 0; i < numberNames.Count; i++)
            // {
            //     Console.WriteLine("key: {0}, value: {1}", numberNames.Keys[i], numberNames.Values[i]);
            // }

            /*
            Remove
            */
            numberNames.Remove(1);
            numberNames.Remove(10);

            //removes key-value pair from index 0
            numberNames.RemoveAt(0);
            //run-time exception: ArgumentOutOfRangeException
            // numberNames.RemoveAt(10);

            foreach (KeyValuePair<int, string> kvp in numberNames)
            {
                Console.WriteLine("key: {0}, value: {1}", kvp.Key, kvp.Value);
            }
        }
    }
}
```
```bash
$ key: 1, value: One
$ key: 2, value: Two
$ key: 3, value: Three
$ key: 4, value:
$ key: 5, value: Five
$ key: 10, value: Ten
$ Two
$ key: 3, value: Three
$ key: 4, value:
$ key: 5, value: Five
```

## SortedDictionary<TKey, TValue> [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.sorteddictionary-2?view=net-6.0)

```csharp
using System;
using System.Collections.Generic;

// namespace
namespace MyBusiness
{
    // main program
    class Program
    {
        static void Main(string[] args)
        {
            // SortedDictionary of int keys, string values
            SortedDictionary<int, string> numberNames = new SortedDictionary<int, string>();

            // Using collection-initializer syntax
            // SortedDictionary<int, string> numberNames = new SortedDictionary<int, string>()
            //                 {
            //                     {3, "Three"},
            //                     {1, "One"},
            //                     {2, "Two"},
            //                 };

            /*
            Add
            */
            numberNames.Add(3, "Three");
            numberNames.Add(1, "One");
            numberNames.Add(2, "Two");
            numberNames.Add(4, null);
            numberNames.Add(10, "Ten");
            numberNames.Add(5, "Five");

            //The following will throw exceptions
            //Compile-time error: key must be int type
            // numberNames.Add("Three", 3);
            //Run-time exception: duplicate key
            // numberNames.Add(1, "One");
            //Run-time exception: key cannot be null
            // numberNames.Add(null, "Five");

            /*
            Access
            */
            foreach (KeyValuePair<int, string> kvp in numberNames)
            {
                Console.WriteLine("key: {0}, value: {1}", kvp.Key, kvp.Value);
            }
            Console.WriteLine(numberNames[2]);
            // Compile error!
            // for (int i = 0; i < numberNames.Count; i++)
            // {
            //     Console.WriteLine("key: {0}, value: {1}", numberNames.Keys[i], numberNames.Values[i]);
            // }

            /*
            Remove
            */
            numberNames.Remove(1);
            numberNames.Remove(10);

            // There is no RemoveAt method
            // numberNames.RemoveAt(0);

            foreach (KeyValuePair<int, string> kvp in numberNames)
            {
                Console.WriteLine("key: {0}, value: {1}", kvp.Key, kvp.Value);
            }
        }
    }
}
```
```bash
$ key: 1, value: One
$ key: 2, value: Two
$ key: 3, value: Three
$ key: 4, value:
$ key: 5, value: Five
$ key: 10, value: Ten
$ Two
$ key: 2, value: Two
$ key: 3, value: Three
$ key: 4, value:
$ key: 5, value: Five
```

## SortedSet [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.sortedset-1?view=net-6.0)

```csharp
using System;
using System.Collections.Generic;

// namespace
namespace MyBusiness
{
    // main program
    class Program
    {
        static void Main(string[] args)
        {
            // SortedSet of string values
            SortedSet<string> sortedSetDemo = new SortedSet<string>();

            //using collection-initializer syntax
            // SortedSet<string> sortedSetDemo = new SortedSet<string>()
            //                 {
            //                     {"Mumbai"},
            //                     {"Surat"},
            //                     {"Vadodara"},
            //                     {"Dabhoi"},
            //                     {"Pune"},
            //                 };

            /*
            Add
            */
            sortedSetDemo.Add("Mumbai");
            sortedSetDemo.Add("Surat");
            sortedSetDemo.Add("Vadodara");
            sortedSetDemo.Add("Dabhoi");
            sortedSetDemo.Add("Pune");

            /*
            Access
            */
            foreach (var item in sortedSetDemo)
            {
                Console.WriteLine(item);
            }

            /*
            Remove
            */
            sortedSetDemo.Remove("Surat");

            foreach (var item in sortedSetDemo)
            {
                Console.WriteLine(item);
            }

            // Clean up the sortedSet
            sortedSetDemo.Clear();

            foreach (var item in sortedSetDemo)
            {
                Console.WriteLine(item);
            }
        }
    }
}
```
```bash
$ Dabhoi
$ Mumbai
$ Pune
$ Surat
$ Vadodara

$ Dabhoi
$ Mumbai
$ Pune
$ Vadodara
```

## Queue [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.queue-1?view=net-6.0)

A **queue** is a collection of entities that are maintained in a sequence and can be modified by the addition of entities at one end of the sequence and the removal of entities from the other end of the sequence.

* First-In First-Out

```csharp
using System;
using System.Collections.Generic;

// namespace
namespace MyBusiness
{
    // main program
    class Program
    {
        static void Main(string[] args)
        {
            //Queue of int values
            Queue<int> intQueue = new Queue<int>();

            /*
            Add
            */
            intQueue.Enqueue(1);
            intQueue.Enqueue(2);
            intQueue.Enqueue(3);
            intQueue.Enqueue(4);

            /*
            Access
            */
            foreach (var id in intQueue)
            {
                Console.Write(id);
            }
            Console.WriteLine("");

            // Peek(): Return the first item from the queue without removing it.
            Console.WriteLine(intQueue.Peek());

            /*
            Remove
            */
            while (intQueue.Count > 0)
            {
                Console.WriteLine(intQueue.Dequeue());
            }
        }
    }
}
```
```bash
$ 1234
$ 1
$ 1
$ 2
$ 3
$ 4
```

## Stack [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.stack-1?view=net-6.0)

* First-In Last-Out

A **Stack** is a linear data structure that follows the LIFO (Last-In-First-Out) principle. Stack has one end, whereas the Queue has two ends (front and rear). It contains only one pointer top pointer pointing to the topmost element of the stack.

```csharp
using System;
using System.Collections.Generic;

// namespace
namespace MyBusiness
{
    // main program
    class Program
    {
        static void Main(string[] args)
        {
            //Stack of int values
            Stack<int> intStack = new Stack<int>();

            /*
            Add
            */
            intStack.Push(1);
            intStack.Push(2);
            intStack.Push(3);
            intStack.Push(4);

            /*
            Access
            */
            foreach (var id in intStack)
            {
                Console.Write(id);
            }
            Console.WriteLine("");

            // Peek(): Return the first item from the queue without removing it.
            Console.WriteLine(intStack.Peek());

            /*
            Remove
            */
            while (intStack.Count > 0)
            {
                Console.WriteLine(intStack.Pop());
            }
        }
    }
}
```
```bash
$ 4321
$ 4
$ 4
$ 3
$ 2
$ 1
```

## LinkedList [Doc](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.linkedlist-1?view=net-6.0)

```csharp
using System;
using System.Collections.Generic;

// namespace
namespace MyBusiness
{
    // main program
    class Program
    {
        static void Main(string[] args)
        {
            // LinkedList of int values
            LinkedList<int> list = new LinkedList<int>();

            /*
            Add
            */
            list.AddLast(1);
            list.AddLast(2);
            LinkedListNode<int> middle = list.AddLast(3);
            list.AddLast(4);
            list.AddLast(5);

            list.AddAfter(middle, 32);
            list.AddAfter(middle, 31);

            /*
            Access
            */
            foreach (int i in list)
            {
                Console.Write("{0}, ", i);
            }
            Console.WriteLine("");
            // Console.WriteLine(middle.Value);
            // Console.WriteLine(middle.Next.Value);

            /*
            Remove
            */
            list.Remove(middle);

            foreach (int i in list)
            {
                Console.Write("{0}, ", i);
            }
            Console.WriteLine("");
        }
    }
}
```
```bash
$ 1, 2, 3, 31, 32, 4, 5,
$ 1, 2, 31, 32, 4, 5,
```

## Using different Collections to do things for you
In class we saw a few progressive examples where just by selecting the right data structure a lot of common tasks in programming can be automated and simplified. Here is the full code:

```csharp

using System;

class Program
{
    static void Main()
    {
        //reading from input
        Console.WriteLine("### Enter a sentence:");
        string input = Console.ReadLine();

        //splitting the input into words and cleaning
        string[] words = input.Split(' ');
        for (int i = 0; i < words.Length; i++)
        {
            words[i] = words[i].ToLower().Trim('.', ',', '!', '?', ';', ':');
        }

        Console.WriteLine("### Cleaned up words:");
        foreach (string word in words)
        {
            Console.Write(word + " ");
        }

        //filtering unique words by using HashShet
        HashSet<string> uniqueWords = new HashSet<string>(words);
        Console.WriteLine("\n### Unique words:");
        foreach (string word in uniqueWords)
        {
            Console.Write(word + " ");
        }
        //sorting them by using SortedSet
        SortedSet<string> sortedWords = new SortedSet<string>(words);
        Console.WriteLine("\n### Sorted words:");
        foreach (string word in sortedWords)
        {
            Console.Write(word + " ");
        }
        //counting individual occurences by using Dictionary
        Dictionary<string, int> wordCount = new Dictionary<string, int>();
        foreach (string word in words)
        {
            if (wordCount.ContainsKey(word))
            {
                wordCount[word]++;
            }
            else
            {
                wordCount[word] = 1;
            }
        }
        //grouping them by first letter
        Dictionary<char, List<string>> wordsByFirstLetter = new Dictionary<char, List<string>>();
        foreach (string word in words)
        {
            char firstLetter = word[0];
            if (wordsByFirstLetter.ContainsKey(firstLetter))
            {
                wordsByFirstLetter[firstLetter].Add(word);
            }
            else
            {
                wordsByFirstLetter[firstLetter] = new List<string> { word };
            }
        }
        Console.WriteLine("\n### Words by first letter:");
        foreach (KeyValuePair<char, List<string>> pair in wordsByFirstLetter)
        {
            Console.WriteLine(pair.Key + ": " + string.Join(", ", pair.Value));
        }
        //selecting the unique words by first letter by using a HashSet instead of List
        Dictionary<char, HashSet<string>> uniqueWordsByFirstLetter = new Dictionary<char, HashSet<string>>();
        foreach (string word in words)
        {
            char firstLetter = word[0];
            if (uniqueWordsByFirstLetter.ContainsKey(firstLetter))
            {
                uniqueWordsByFirstLetter[firstLetter].Add(word);
            }
            else
            {
                uniqueWordsByFirstLetter[firstLetter] = new HashSet<string> { word };
            }
        }
        Console.WriteLine("\n### Unique words by first letter:");
        foreach (KeyValuePair<char, HashSet<string>> pair in uniqueWordsByFirstLetter)
        {
            Console.WriteLine(pair.Key + ": " + string.Join(", ", pair.Value));
        }
    }

}

```
---
# Selected Theory

# Complexity Theory
## Sequential/Linear Search vs. Binary Search [Doc](https://www.tutorialspoint.com/comparison-of-searching-methods-in-data-structures)

## Big O Notation [Doc](https://en.wikipedia.org/wiki/Big_O_notation)
Big O notation is a mathematical notation that describes the limiting behavior of a function when the argument tends towards a particular value or infinity.

## SortedList vs. SortedDictionary

The SortedDictionary<TKey, TValue> generic class is a binary search tree with O(log n) retrieval, where n is the number of elements in the dictionary. In this, it is similar to the  SortedList<TKey, TValue> generic class. The two classes have similar object models, and both have O(log n) retrieval. Where the two classes differ is in memory use and speed of insertion and removal:

* SortedList<TKey, TValue> uses less memory than SortedDictionary<TKey, TValue>.
* SortedDictionary<TKey, TValue> has faster insertion and removal operations for unsorted data, O(log n) as opposed to O(n) for  SortedList<TKey, TValue>.
* If the list is populated all at once from sorted data, SortedList<TKey, TValue> is faster than  SortedDictionary<TKey, TValue>.

|------------------|---------|----------|--------|----------|----------|---------|
| Collection       | Indexed | Keyed    | Value  | Addition |  Removal | Memory  |
|                  | lookup  | lookup   | lookup |          |          |         |
|------------------|---------|----------|--------|----------|----------|---------|
| SortedList       | O(1)    | O(log n) | O(n)   | O(n)     | O(n)     | Lesser  |
| SortedDictionary | O(n)    | O(log n) | O(n)   | O(log n) | O(log n) | Greater |
|------------------|---------|----------|--------|----------|----------|---------|




