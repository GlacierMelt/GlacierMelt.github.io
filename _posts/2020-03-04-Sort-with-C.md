---
layout: post
title: "Sort with C"
date: 2020-03-04 15:05:18 +020
tags: [guide]
image: 9.jpg
categories: guide
---
# C 排序算法的实现
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
## Merge Sort
```C
void MergeSort(int *A, int lo, int hi){
    if(lo >= hi) return;
    int mid = lo + (hi - lo) / 2;
    MergeSort(A, lo, mid);
    MergeSort(A, mid, hi);
    merge(A, lo, mid, hi);
}

void merge(int *nums, int lo, int mid, int hi){
    int[] copy = nums.clone();
    int k = lo, i = lo, j = mid+1;
    while(k <= hi){
        if(i > mid){
            nums[k++] = copy[j++];
        }else if(j > hi){
            nums[k++] = copy[i++];
        }else if(copy[j] < copy[i]){
            nums[k++] = copy[j++];
        }else{
            nums[k++] = copy[i++];
        }
    }
}
```
## Quick Sort
```C
void QuickSort(int nums[], int lo, int hi){
    if(lo >= hi) return;
    int p = partition(nums, lo, hi);
    QuickSort(nums, lo, p-1);
    QuickSort(nums, p+1, hi);
}

int partition(int nums[], int lo, int hi){
    int i, j;
    for(i=lo, j=lo; j<hi; j++){
        if(nums[j] <= nums[hi]){
            swap(nums, i++, j);       
        }
    }
    swap(nums, i, j);
    return i;
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
	InsertionSort(array, lenght);
	QuickSort(array, 0, lenght-1);
  	for(int i=0; i<lenght-1; i++)
            printf("%d ", array[i]);
    return 0;
}
```
