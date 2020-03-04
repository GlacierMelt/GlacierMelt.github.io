---
layout: post
title: "Sort with C"
date: 2020-03-04 15:05:18 +020
tags: [guide]
categories: guide
---
# Bubble Sort
```C
#include <stdio.h>

void swap(int nums[], int a, int b){
  int temp = *(nums+a);
  *(nums+a) = *(nums+b);
  *(nums+b) = temp;
}

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

int main(){
  	int array[] = {0, 9, 10, 45, 21, 77, 36, 13, 11, 5};
  	int lenght = sizeof(array) / sizeof(array[0]);
	Bubblesort(array, lenght);
  	for(int i=0; i<lenght-1; i++)
      printf("%d ", array[i]);
    return 0;
}
```
