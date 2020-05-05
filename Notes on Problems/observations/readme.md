
**Duplicates in an array**

If we have to choose 2 elements in an array such that a condition is satisfied (converging 2 pointer pattern) and the elements must be unique do the following:

- Sort the array and start 2 pointers
- If left pointer is not the start and left is not equal to its previous element **OR** right pointer is not end and right is not equal to next element, increment/decrement the pointers.
- Otherwise do the operation.

This comes up in [3Sum](https://leetcode.com/problems/3sum/) problem.
