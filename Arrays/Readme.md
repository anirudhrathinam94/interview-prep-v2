
### Cumulative Best

**Overview**

In this pattern we first create a separate array - this is the cumulative best array `a[0...n]`. Then we scan the input array `input[0...n]` let's say from left to right and as we scan, we fill in `a[i]` with the best value seen so far from `input[0...i]`. The pattern is as follows:

- Initialize the cumulative best array `a[]` with same size as input
- In the loop if `i=0` then `a[i] = input[i]` since the best from `input[0...0]` is `input[0]`
- Otherwise `a[i] = best(a[i-1], input[i])` since `a[i-1]` contains the best from `input[0...i-1]`

**Use cases**

This is useful anytime we need the best value from one (or more) direction more than once when solving the problem. Some examples are as follows:

- Prefix sum with changing inputs: Given an array compute the sum of elements from a[i...j] where i and j can change. In this case the cumulative best should have the cumulative sum.
- [Trapping rain water](https://leetcode.com/problems/trapping-rain-water): In the brute force approach for every position i in the array the amount of rainwater that it can hold is:
  - min of `tallest bar seen from left of i` and `tallest bar seen from left of i` minus `a[i]`
  - So here we have 2 cumulative best arrays holding best height seen so far from left and best height seen so far from right

The code for trapping rain water is below:

    public int trap(int[] a) {
        int[] left = new int[a.length];
        int[] right = new int[a.length];
        
        for(int i=0; i<a.length; i++) {
            if(i == 0)
                left[i] = a[i];
            else
                left[i] = Math.max(a[i], left[i-1]);
        }
        
        for(int i=a.length-1; i >= 0; i--) {
            if(i==a.length-1)
                right[i] = a[i];
            else
                right[i] = Math.max(a[i], right[i+1]);
        }
        
        int sum = 0;
        
        for(int i=0; i<a.length; i++) {
            sum += Math.min(left[i], right[i]) - a[i];
        }
        return sum;
    }
