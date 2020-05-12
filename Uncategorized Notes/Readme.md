
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

### The general search pattern

For many problems it is easier to validate against the edges of the search space. If we were to validate against the edges of the search space for general binary search the algorithm would be:

- Get the pivot (mid) and validate against the target. If `a[mid] = target` return.
- Otherwise look at the left of the pivot and validate target against `a[lo] ... a[mid-1]` by comparing against the edges. 
- If target could exist between `a[lo] ... a[mid-1]` recurse over the search space otherwise recurse over the other half.

The code for this is:

    private int binarySearch(int[] a, int tgt, int lo, int hi) {
        if(lo > hi)
            return -1;
        int mid = (lo + hi) / 2;
        if(a[mid] == tgt)
            return mid;
        else if(tgt >= a[lo] && tgt < a[mid])
            return binarySearch(a, tgt, lo, mid-1);
        else
            return binarySearch(a, tgt, mid+1, hi);
    }

For regular binary search, we do not validate against the boundaries because it is obvious what the search space is. However there are many problems with structured inputs that are not sorted and for these problems, it is necessary to validate against the search space.

**NOTE: When doing comparisons like `if(tgt >= a[lo] && tgt < a[mid])` avoid adding/subtracting anything to mid or you will have an array out of bounds error. It should NOT be `if(tgt >= a[lo] && tgt <= a[mid-1])` or we will get error**

------------------

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

Treat each row/col as an individual array. 
- We first identify what row to search by doing a binary search for tgt on the 0th column. If we find tgt in 0th column, then return mid. If we dont find it we can use the fact that **the search ends when `lo > hi` meaning `a[hi] < tgt < a[lo]`** and return `lo-1` as the row we need to search.
- Then do a binary search on the row we identified to find the target.

Code is below:

    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix.length == 0 || matrix[0].length == 0)
            return false;
        int row = searchRow(matrix, target);
        if(row < 0)
            return false;
        return searchCol(matrix, target, row);
    }
    
    private int searchRow(int[][] a, int tgt) {
        int lo = 0;
        int hi = a.length-1;
        while(lo <= hi) {
            int mid = (lo+hi)/2;
            if(a[mid][0] == tgt)
                return mid;
            else if(a[mid][0] > tgt)
                hi = mid-1;
            else
                lo = mid+1;
        }
        return lo - 1;
    }
    
    private boolean searchCol(int[][] a, int tgt, int row) {
        int lo = 0;
        int hi = a[0].length-1;
        while(lo <= hi) {
            int mid = (lo+hi)/2;
            if(a[row][mid] == tgt)
                return true;
            else if(a[row][mid] > tgt)
                hi = mid-1;
            else
                lo = mid+1;
        }
        return false;
    }


----------

### Binary Search with modified input structure

These have structured input however are not strictly sorted. The trick to a lot of these problems is to validate against the edges of the search space.

**[Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)**

One of either `lo...mid` is sorted OR `mid...hi` has to be sorted. See what half is sorted and for the sorted half see if the target can lie within the edges. Recurse accordingly.

    private int binarySearch(int[] a, int tgt, int lo, int hi) {
        if(lo > hi)
            return -1;
        int mid = (lo+hi)/2;
        if(a[mid] == tgt)
            return mid;
        else if(a[mid] < a[hi]) {
            if(tgt > a[mid] && tgt <= a[hi])
                return binarySearch(a, tgt, mid+1, hi);
            else
                return binarySearch(a, tgt, lo, mid-1);
        } else {
            if(tgt >= a[lo] && tgt < a[mid])
                return binarySearch(a, tgt, lo, mid-1);
            else
                return binarySearch(a, tgt, mid+1, hi);
        }
    }

-------------

**[Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)**

The loop ends when `lo > hi`. This means `a[hi] < tgt < a[lo]` this condition holds even for rotated sorted arrays because towards the end, the subarray is of size 1 (aka a sorted array). In this casse a[lo] will always hold the smallest value (imagine the tgt is min value).

    private int binarySearch(int[] a, int lo, int hi) {
        if(lo > hi)
            return a[lo];
        int mid = (lo+hi)/2;
        if(isLeast(a, mid))
            return a[mid];
        if(a[mid] < a[hi])
            return binarySearch(a, lo, mid-1);
        else
            return binarySearch(a, mid+1, hi);
    }
    
    private boolean isLeast(int[] a, int mid) {
        int l = mid-1 < 0? Integer.MAX_VALUE: a[mid-1];
        int r = mid+1 >= a.length? Integer.MAX_VALUE: a[mid+1];
        if(a[mid] < l && a[mid] < r)
            return true;
        return false;
    }


