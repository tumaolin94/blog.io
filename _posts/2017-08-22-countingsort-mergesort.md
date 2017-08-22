---
layout: post
title: Counting Sort in JAVA
date: 2017-08-22
categories: blog
tags: [Data Struct, algorithm, Sort]
description: 	

---

# Counting Sort

There is a detailed explanation in the book `In troduction to Algorighms, Third Edition` and Wikipedia.

[Counting Sort](https://en.wikipedia.org/wiki/Counting_sort) owns O(k+n) time complecity in average, while `k` is the size of total number we could use to sort and `n` is the size of unsorted array.

We need at list three array to complete the sort. input array, count array and output array.

For simplicity, assume the input data in the range 0 to 9. 
Input data: 2, 5, 3, 0, 2, 3, 0, 3
  1) Take a count array to store the count of each unique object.
  Index:     0  1  2  3  4  5  6  7  8  9
  Count:     2  0  2  3  0  1  0  0  0  0

  2) Modify the count array such that each element at each index 
  stores the sum of previous counts. 
  Index:     0  1  2  3  4  5  6  7  8  9
  Count:     2  2  4  6  7  8  8  8  8  8

The modified count array indicates the position of each object in 
the output sequence.
 
  3) Output each object from the input sequence followed by 
  decreasing its count by 1.

## Code
The simple code is following:
```
public // Java implementation of Counting Sort
class CountingSort
{
	//arr is input array. base is calculated range
    public int[] sort(int arr[], int base)
    {
        int n = arr.length;
 
        // The output array that will have sorted arr
        int[] output = new int[n];
 
        // Create a count array to store count of inidividul
        // characters and initialize count array as 0
        int count[] = new int[base+1];
        for (int i=0; i<base; i++)
            count[i] = 0;
 
        // store count of each integer
        for (int i=0; i<n; i++)
            ++count[arr[i]];
 
        // Change count[i] so that count[i] now contains actual
        // position of this number in output array
        for (int i=1; i<=base; i++)
            count[i] += count[i-1];
 
        // Build the output array
        for (int i = 0; i<n; i++){
//        	System.out.println(i+" "+arr[i]+" "+ count[arr[i]]);
            output[count[arr[i]]-1] = arr[i];
            count[arr[i]]--;
        }
 
        return output;
    }
    
    public static void main(String args[])
    {
        CountingSort ob = new CountingSort();
       int[] arr = {2,5,3,0,2,3,0,3};
       int base = 9;
       int[]  res = ob.sort(arr,base);
 
        System.out.print("Sorted integer array is ");
        for (int i=0; i<arr.length; i++)
            System.out.print(res[i]+" ");
    }
}
```
