---
layout: post
title: "Some Sort Algorithms Implementation"
categories : Algorithms
tags : CPP Algorithms
---

* content
{:toc}

MergeSort is a Divide and Conquer algorithm. It divides input array in two halves, calls itself for the two halves and then merges the two sorted halves. 

![](/images/algorithms/merge.png)

## Codes
```cpp
#include <iostream>
using namespace std;
void merge(int arr[], int l, int m, int r) {
    int l1 = m-l+1, l2 = r-m;
    int L[l1], R[l2];
    int i, j, k;
    for (i=0; i<l1; i++)
        L[i] = arr[l+i];
    for (j=0; j<l2; j++)
        R[j] = arr[m+1+j];
    
    i=0;
    j=0;
    k=l;
    while (i<l1 || j<l2) {
        if (i<l1 && j<l2) {
            if (L[i] < R[j])
                arr[k++] = L[i++];
            else
                arr[k++] = R[j++];
        }
        else if (i<l1)
            arr[k++] = L[i++];
        else
            arr[k++] = R[j++];
    }
    
    
}

void mergeSort(int arr[], int l, int r) {
    if (l<r) {
        int m = l+(r-l)/2;
        mergeSort(arr, l, m);
        mergeSort(arr, m+1, r);
        merge(arr, l, m, r);
    }
}

void printArray(int arr[], int n) {
    for (int i=0; i<n; i++)
        cout << arr[i] << " ";
    cout << endl;
}

int main() {
    int arr[] = {13, 4, 53, 11, 20, 23};
    int size = sizeof(arr)/sizeof(arr[0]);
    mergeSort(arr, 0, size);
    printArray(arr, size);
    return 1;
}
```