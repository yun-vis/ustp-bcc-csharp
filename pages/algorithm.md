---
# permalink: /about/
layout: single
title: "Algorithm"
classes: wide
header:
  image: /assets/images/teaser/teaser.png
  caption: "Image credit: [**Yun**](http://yun-vis.net)"
last_modified_at: 2026-03-05
---

# What is Algorithm?
An algorithm is a precise, step-by-step set of instructions or rules designed to accomplish a specific task or solve a problem. It takes an input, processes it through a defined series of finite steps, and produces a desired output. 

# Sorting Algorithms

A Sorting Algorithm is used to rearrange a given array or list of elements in an order. For example, a given array [10, 20, 5, 2] becomes [2, 5, 10, 20] after sorting in increasing order and becomes [20, 10, 5, 2] after sorting in decreasing order.

## Quick Sort

In MyBusiness/Program.cs
```csharp
using AlgorithmLibrary.QuickSort;

namespace MyBusiness;

class Program
{
    static void Main(string[] args)
    {
        int[] myArray = { 10, 7, 8, 9, 1, 5 };

        QuickSort.Sort(myArray, 3, myArray.Length - 1);

        foreach (int val in myArray)
        {
            Console.Write(val + " ");
        }

    }
}
```
```bash
The singlyLinkedList: 2 6 4 
```

In AlgorithmLibrary/QuickSort.cs
```csharp
namespace AlgorithmLibrary.QuickSort;

public class QuickSort
{
    public QuickSort()
    {
    }

    // partition function
    static int _partition(int[] arr, int low, int high)
    {

        // choose the pivot
        int pivot = arr[high];

        // index of smaller element and indicates 
        // the right position of pivot found so far
        int i = low - 1;

        // traverse arr[low..high] and move all smaller
        // elements to the left side. Elements from low to 
        // i are smaller after every iteration
        for (int j = low; j <= high - 1; j++)
        {
            if (arr[j] < pivot)
            {
                i++;
                _swap(arr, i, j);
            }
        }

        // move pivot after smaller elements and
        // return its position
        _swap(arr, i + 1, high);
        return i + 1;
    }

    // swap function
    static void _swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // The QuickSort function implementation
    public static void Sort(int[] arr, int low, int high)
    {
        if (low < high)
        {

            // pi is the partition return index of pivot
            int pi = _partition(arr, low, high);

            // recursion calls for smaller elements
            // and greater or equals elements
            Sort(arr, low, pi - 1);
            Sort(arr, pi + 1, high);
        }
    }
}
```

---
# External Resources

## [Sorting Algorithms](https://www.geeksforgeeks.org/dsa/sorting-algorithms/)

## [Functional Programming](https://learn.microsoft.com/en-us/archive/msdn-magazine/2009/october/functional-programming-for-everyday-net-development)
