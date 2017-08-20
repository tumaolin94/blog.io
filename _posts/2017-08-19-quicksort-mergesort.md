---
2	layout: post
3	title: QuickSort and MergeSort in JAVA
4	date: 2017-08-19
5	categories: blog
6	tags: [Data Struct, algorithm, Sort]
7	description: 
8	
9	---

# QuickSort
QuickSort is a very famous sort algorithm, `Arrays.sort` is realized by QuickSort.

## Overview

The basic method is following:
1. Choosing a `pivot`, always the lowest value.
2. Dividing the array into two parts, the lower part will be put left of the `pivot`, and the larger part is right.
3. With each round, the `pivot` will move to the final position in the array.
4. Repeat the process, until the sort is completed.
 
## Code in JAVA

```
	public void qsort(int[] arr, int low, int high) {
		if(low<high) {
			//	Set the position of pivot
			int pivot = partition(arr, low, high);
            // QuickSort the left part and the right part respectively
			qsort(arr, low, pivot-1);
			qsort(arr, pivot+1, high);
			
		}
	}
	
	public int partition(int[] arr, int low, int high) {
	// search and set the position of the pivot
		int pivot = arr[low];
		
		while(low<high) {
			while(low<high&&arr[high]>=pivot) high--;
			arr[low] = arr[high];
			while(low<high&&arr[low]<=pivot) low++;
			arr[high]=arr[low];
		}
		
		arr[low]=pivot;
		
		return low;
	}
```

# MergeSort

## Overview

Conceptually, a merge sort works as follows:

1. Divide the unsorted list into n sublists, each containing 1 element (a list of 1 element is considered sorted).
2. Repeatedly merge sublists to produce new sorted sublists until there is only 1 sublist remaining. This will be the sorted list.

## Code in JAVA

```
	public void mergeSort(int[] arr, int[] temp, int low, int high) {
		if(low<high) {
			int middle = low+(high-low)/2;
			mergeSort(arr, temp, low, middle);
			mergeSort(arr, temp, middle+1, high);
			mergeSortedArray(arr, temp, low, middle, high);
		}
	}
	
	public void mergeSortedArray(int[]arr, int[] temp, int low, int middle, int high) {
		int i= low;
		int j=middle+1;
		int k = 0;
		while(i<=middle&&j<=high) {
			if(arr[i]<=arr[j]) {
				temp[k++] = arr[i++];
			}
			else {
				temp[k++] = arr[j++];
			}
		}
		while(i<=middle) temp[k++] = arr[i++];
		while(j<=high) temp[k++]  = arr[j++];
		for(i=0;i<k;i++) {
			arr[low+i] = temp[i];
		}
	}
```

## Analysis

In sorting n objects, merge sort has an average and worst-case performance of O(n log n). If the running time of merge sort for a list of length n is T(n), then the recurrence T(n) = 2T(n/2) + n follows from the definition of the algorithm (apply the algorithm to two lists of half the size of the original list, and add the n steps taken to merge the resulting two lists). The closed form follows from the master theorem.

# Compare

QuickSort has two major deficiencies when compared to mergesort:

1. It’s not stable (as parsifal noted).

2. It doesn’t guarantee n log n performance; it can degrade to quadratic performance on pathological inputs.

and a detailed comparison is following
(From WiKiPedia):

![Sort](https://raw.githubusercontent.com/tumaolin94/tumaolin94.github.io/master/img/sort.jpg)
