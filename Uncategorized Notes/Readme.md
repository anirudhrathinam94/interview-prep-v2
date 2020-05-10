
These should be categorized after completing the relevant study material.

-------------

## Divide and Conquer

Divide and conquer tries to divide an array in half and recurses on either left half or right half or both.

-----------

### Binary Search

Input is structured in some way and we can take advantage of this by pruning the search space in half for each iteration. Here array is sorted. Look for target in aray and return -1 if not present.

**Recursive**

Code is below:
    
    private int binarySearch(int[] a, int target, int lo, int hi) {
        if(lo > hi)
            return -1;
        int mid = (lo+hi)/2;
        if(a[mid] == target)
            return mid;
        else if(target < a[mid])
            return binarySearch(a, target, lo, mid-1);
        else
            return binarySearch(a, target, mid+1, hi);
    }

**Iterative**

Code is below:

    public int search(int[] a, int target) {
        int lo = 0;
        int hi = a.length-1;
        while(lo <= hi) {
            int mid = (lo+hi)/2;
            if(a[mid] == target)
                return mid;
            else if(target > a[mid])
                lo = mid+1;
            else
                hi = mid-1;
        }
        return -1;
    }
    
----------    

### QuickSort and Mergesort

This only covers the divide and conquer parts of the algorithm. 
- For quicksort partition chooses an element and places all elements less than it in the left and elements greater than it in the right. See 2 pointer section for more info.
- For mergesort, the merge function merges 2 sorted lists into 1 sorted list.

**MergeSort**

The algorithm is:

    private void mergesort(int[] a, int[] b, int lo, int hi) {
        if(lo < hi) {
            int mid = (lo+hi)/2;
            mergesort(a, b, lo, mid);
            mergesort(a, b, mid+1, hi);
            merge(a, b, lo, mid, hi);
        }
    }

**Quicksort**

The algorithm is:

    private void quicksort(int[] a, int lo, int hi) {
        if(lo < hi) {
            int p = partition(a, lo, hi);
            quicksort(a, lo, p-1);
            quicksort(a, p+1, hi);
        }
    }

-----------

### Invariants in Divide and Conquer Algirithms 

A common error in Divide and Conquer algorithms like Binary Search, Quicksort and Mergesort is the off-by-one error. To avoid this we need to think of the invariant before we recurse.

For binary search the invariant is do the algorithm only if `lo <= hi`.
- It does not work for `lo < hi` because then we ignore single element arrays.

For merge sort the invariant is `lo < hi`.
- It does not work for `lo<=hi` because once we divide, we sort the left and the right subarrays. Then we try to merge the second array starting from mid+1 which causes an out of bounds exception.

For quick sort the invariant is `lo < hi` or `lo <= hi`
- In the case of quicksort `lo<=hi` will work because we partition then try to sort left half and right half both of which dont exist as `lo > hi` and the recurrence is immediately rejected.

Choosing a valid invariant:
- An easy way to think about what a valid invariant can be is to consider the problem in terms of a single element array where `lo = hi`
  - In binary search we still need to search the single array so the invariant can be: do it if `lo <= hi`
  - For the sort algorithms, we get the mid and we perform actions on the left and right subarrays. For mergesort the right subarray does not exist and for quicksort both the left and right subarrays do not exist so the invariant can be: do it if `lo < hi`
  
