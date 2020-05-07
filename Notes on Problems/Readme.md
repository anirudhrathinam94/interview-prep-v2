
## Overview

This page documents a 2-3 sentence summary on several problems I have done on Leetcode.

----------

## Problems

#### 1. Two Sum
To do it in 2 loops store all items in map (first loop) and search for tgt-i (second loop).
To do it in one loop check if map contains i. If not store tgt-i in map.

#### 2. Add 2 numbers
Loop through 2 lists storing sum in third list.

#### 3. Longest substring without repeating characters
Initialize 2 pointers starting at 0. Keep increasing fast pointer until end of loop or until condition is violated. If condition is violated increment slow pointer until condition is satisfied.
**Note: Careful about index out of bounds errors for right pointer**

#### 5. Longest Palindromic Substring
Regular DP problem. Expand from the center. f(i,j) is true if i=j and f(i+1, j-1) os true. 
**NOTE: Careful about the case cbbd - consider even palindromes when doing bottom up**

#### 7. Reverse Integer
Do `sum = sum*10 + x%10; x = x/10`. Be sure to make sure that sum lies within 32 bit int range (ie make sure sum is a long not an int).

#### 8. Integer to String (atoi)
[Need to do this].

#### 9. Palindrome Number
Return false for negative integer. Reverse the integer storing val in a long by doing `sum = sum*10 + x%10; x = x/10`. If sum is more than max int return false else return `(int)sum == x`.

#### 10. Regular Expression Matching
Regular DP problem. Has a bunch of cases (when characters match/dont match, when next character is a * etc) so recurrence relation will be huge.

#### 11. Container with most water
Initialize two pointers at both ends and loop while pointers dont converge. Compare current heights and greedily advance the height that is smaller calculating area at each step.

#### 13. Roman to Integer
[Need to do this]

#### 14. Longest common prefix
Basic Recursion. `f(prefix, index) = f( getPrefix(prefix, array[index]), index+1 )`.

#### 15. 3Sum
Converging 2 pointer. Outer loop iterates from `i=0 ... i < n-2`. Elements from `i+1...n` are covered bby 2 pointer. Duplicates are eleminated by the sorting technique (see observations).

#### 16. 3Sum Closest
Same as 3Sum except easier because you dont need to care about duplicates. Maintain a min value to keep track of min and update accordingly.

#### 19. Remove Nth Node From End of List
Initialize dummy node before head to deal with edge cases. Initialize p1, p2 at dummy and move p2 'n' times. Then until p2 next is not null move both p1, p2. This places p1 in the node before the node to be deleted. If that node is head then p1 point to dummy. Return `dummy.next`.

#### 20. Valid Parantheses
Use stack. For multiple bracket types use stack, for single bracket type we can use counter as well. This is multiple bracket types so stack must be used.

#### 21. Merge Two Sorted Lists
Use recursion. `f(l1, l2) = f(l1.next, l2) if l1 < l2 OR f(l1, l2.next) if l1 > l2`.  This does it in place.

#### 22. Generate Parentheses
Standard backtracking problem. Set i, j as counts for open/close brackets. If i and j equals n then add to list and return. If `i < n` then add open bracket, do `f(i+1, j)` and remove open bracket (backtrack). If `i > j` then add close bracket, do `f(i, j+1)` and remove close bracket (backtrack). We need to do both these operations.

#### 23. Merge k Sorted Lists
Two ways to do this in Nlog(k) complexity. 
1. Using heap: Trivial. Create heap of size k that holds ListNodes and add first of each list. Pop heap, add min node's next to heap until heap is empty. Space is O(k).
2. Mergesort: `f(lists, lo, hi)` stores result list in `lists[lo]`. If `lo < hi` call `f(lists, lo, mid)` and `f(lists, mid+1, hi)`. Then merge lists from `list[lo]` and `list[mid+1]` and store it in `list[lo]`. **invariant is: lo < hi** and the space is O(1).

#### 24. Swap Nodes in Pairs
Initialize dummy node before head. define `f(node)` such that `[node.next ... tail]` will be swapped. Call `f(dummy)` and return `dummy.next`.
