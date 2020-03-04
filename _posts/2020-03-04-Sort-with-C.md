---
layout: post
title: "Sort with C"
date: 2020-03-04 15:05:18 +020
tags: [guide]
image: 11.jpg
categories: guide
---
# C 排序算法的实现
| Sort   | Worst Case    | Average Case   	| Best Case        | 
| -------------		 |:-------------: |:-------------:	| -----:    |
|  [Bogo](https://en.wikipedia.org/wiki/Bogosort)   			| O((n+1)!)	|O((n+1)!)   | O(n)	|
|  [Bubble](https://en.wikipedia.org/wiki/Bubble_sort)  		| O(n<sup>2</sup>)|	O(n<sup>2</sup>) | O(n)		|
|  [Cocktail Shaker](https://en.wikipedia.org/wiki/Cocktail_shaker_sort)| O(n<sup>2</sup>) |O(n<sup>2</sup>)	| O(n)		|
|  [Selection](https://en.wikipedia.org/wiki/Selection_sort)   		| O(n<sup>2</sup>) |O(n<sup>2</sup>) | O(n<sup>2</sup>)	|
|  [Gnome](https://en.wikipedia.org/wiki/Gnome_sort)   		        | O(n<sup>2</sup>)|	O(n<sup>2</sup>) |  O(n<sup>2</sup>)|
|  [Comb](https://en.wikipedia.org/wiki/Comb_sort)   			| O(n<sup>2</sup>) |O(nlogn) |O(nlogn)  	|
|  [Insertion](https://en.wikipedia.org/wiki/Insertion_sort)   		| O(n<sup>2</sup>)|	O(n<sup>2</sup>) |O(n)	|
|  [Shell](https://en.wikipedia.org/wiki/Shellsort)   			| O(n(log(n))<sup>2</sup>) | O(n(log(n))<sup>2</sup>)|O(nlogn)	|
|  [Merge Sort](https://en.wikipedia.org/wiki/Merge_sort)  		| O(nlogn)	| O(nlogn)		 |O(nlogn)            |	
|  [Quick Sort](https://en.wikipedia.org/wiki/Quicksort)   		| O(n<sup>2</sup>)| 	O(nlogn)	|O(nlogn)    	|
|  [Heap Sort](https://en.wikipedia.org/wiki/Heapsort)   		| O(nlogn)|	 O(nlogn)	 |O(nlogn)     	|
## Bubble Sort
```C
void Bubblesort(int *nums, int lenght){
    int hasChange = 1;
    for(int i=0; i<lenght-1 && hasChange; i++){
        hasChange = 0;
        for(int j=0; j<lenght-1-i; j++){
            if(nums[j] > nums[j+1]){
                swap(nums, j, j+1);
                hasChange = 1;
            }
        }
    }
}
```
## Insertion Sort
```C
void InsertionSort(int *nums, int lenght){
    for(int i=1, j, current; i<lenght; i++){
        current = nums[i];
        for(j=i-1; j>=0 && nums[j]>current; j--){
            nums[j+1] = nums[j];
        }
        nums[j+1] = current;
    }
}
```
## Remaining code
```C
#include <stdio.h>

void swap(int nums[], int a, int b){
  int temp = *(nums+a);
  *(nums+a) = *(nums+b);
  *(nums+b) = temp;
}

int main(){
  	int array[] = {0, 9, 10, 45, 21, 77, 36, 13, 11, 5};
  	int lenght = sizeof(array) / sizeof(array[0]);
	Bubblesort(array, lenght);
  	for(int i=0; i<lenght-1; i++)
      printf("%d ", array[i]);
    return 0;
}
```
