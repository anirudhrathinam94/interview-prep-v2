
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
 
**Observations**

- Here, the following happens: we choose a mid and compare it to the target. If mid is smaller we choose the subarray **after** mid and if mid is larger, we choose the subarray **before** mid. It is important to realize that **mid itself may not included in the recursive calls if there is no match**.

- Another observation is that **if target is not present in the array lo is where the target would have been if it was in the array**. This can be observed by looking at how lo changes.
  - What this means is that **if the element is not found the loop ends when `hi < lo` such that `a[hi] < target < a[lo]`**

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

A common error in Divide and Conquer algorithms like Binary Search, Quicksort and Mergesort is the off-by-one error. To avoid this we need to think of the invariant before we recurse. The thought process in choosing a valid invariant is as follows:

- Consider the problem in terms of a single element array where `lo = hi`
  - In binary search we still need to search the single array so the invariant can be: do it if `lo <= hi`
  - For the sort algorithms, a single element array is already sorted. Additionally we get the mid and we perform actions on the left and right subarrays. For mergesort the right subarray does not exist and for quicksort both the left and right subarrays do not exist so the invariant can be: do it if `lo < hi` (although quicksort also supports `lo <= hi`)
- The complication here is with mergesort. The problem is that we have recurrence calls before actually calling the merge.
  
--------------

## Binary Search and related algorithms

### Binary Search direct variants

Some binary search variants are below

**[Search Insert Position](https://leetcode.com/problems/search-insert-position/)**

The trick is understanding the termination condition for binary search and the values held by a[lo] and a[hi] after the loop terminates. The loop ends when `lo > hi`. Since the array is sorted it means that `a[hi] < target < a[lo]` by the time the loop ends.

    public int searchInsert(int[] a, int target) {
        int lo = 0;
        int hi = a.length-1;
        while(lo <= hi) {
            int mid = (lo+hi)/2;
            if(a[mid] == target)
                return mid;
            if(a[mid] > target)
                hi = mid-1;
            else
                lo = mid+1;
        }
        return lo;
    }


------------

**[Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)**

Do not stop when first instance of mid is found. If `tgt = a[mid]` do not return but continue to search in the left and right of mid. Return only when `lo > hi`. It is easier to do this recursively because when `tgt = a[mid]` we search both sides and not just 1 side.

    private void search(int[] nums, int target, int lo, int hi) {
        if(lo > hi)
            return;
        int mid = (lo+hi)/2;
        if(nums[mid] == target) {
            p1 = Math.min(p1, mid);
            p2 = Math.max(p2, mid);
            search(nums, target, mid+1, hi);
            search(nums, target, lo, mid-1);
        } else if(nums[mid] > target)
            search(nums, target, lo, mid-1);
        else
            search(nums, target, mid+1, hi);
    }

-------------

**[Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)**


----------

### Binary Search with modified input structure

