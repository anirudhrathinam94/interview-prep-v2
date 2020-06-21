
### Cumulative arrays and Prefix Sums

**Cumulative Array**

Given an array, we run over the array aggregating the values until `a[0...i]` and store it in another array `c[i]`. Here `c[i]` is the cumulative array. It is used to eleminate repetition (dp) in problems where we need to repeatedly iterate over i.

------------------

**Prefix sums**

Prefix sums are cumulative arrays where we do a cumulative addition like so:

    for(int i=0; i<a.length; i++)
        prefix[i] = i == 0? a[i] : a[i] + prefix[i-1];
  
This helps us answer range sum queries such as what are the sum of elements in the array between i, j inclusive in constant time. This is given by the following equation: `sum = prefix[j] - prefix[i-1]`

-----------------

**N prefix sums**

There are several prefix sum problems that require us to perform prefix sum operations for all possible values of i,j. In a lot of these cases we are comparing the prefix sum against another value k. Some examples are: 

- number of i,j pairs with sum = k 
- smallest i,j subarray with sum >= k and so on

If we naively choose all values of i,j and validate the prefix sum against k, we have a solution with n^2 complexity. However since we know the value of k, we can use this knowledge to drive down the complexity.

---------------

- https://leetcode.com/problems/minimum-size-subarray-sum/

- https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k/
- https://leetcode.com/problems/maximum-size-subarray-sum-equals-k/



- https://leetcode.com/problems/trapping-rain-water/
- https://leetcode.com/problems/subarray-sum-equals-k/
- https://leetcode.com/problems/remove-zero-sum-consecutive-nodes-from-linked-list/
- https://leetcode.com/problems/subarray-sums-divisible-by-k/
