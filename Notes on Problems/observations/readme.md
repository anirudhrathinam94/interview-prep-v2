
**Duplicates in an array**

If we have to choose 2 elements in an array such that a condition is satisfied (converging 2 pointer pattern) and **if the elements must be unique** do the following:

- Sort the array and start 2 pointers
- If left pointer is not the start and left is not equal to its previous element **OR** right pointer is not end and right is not equal to next element, increment/decrement the pointers.
- Otherwise do the operation.

This comes up in [3Sum](https://leetcode.com/problems/3sum/) problem.

**Edge cases for Linked List problems involving traversal/deletion**

Some problems require traversing the list and deleting a node. In many cases this node might be the head. So to bypass edge cases due to this create a new dummy node before the head and do all operations starting from dummy instead of head.

In the end return dummy.next instead of head.
