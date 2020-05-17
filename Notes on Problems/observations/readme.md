
**Duplicates in an array**

If we have to choose elements in an array such that a condition is satisfied and **if the elements must be unique** do the following:

- Sort the array
- If the current element/elements we are processing is NOT the first element it was initialized and if a[i] = a[i-1] then go to the next element.

Problems this comes up in include:

- [3Sum](https://leetcode.com/problems/3sum/) problem.
- [Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)


**Edge cases for Linked List problems involving traversal/deletion**

Some problems require traversing the list and deleting a node. In many cases this node might be the head. So to bypass edge cases due to this create a new dummy node before the head and do all operations starting from dummy instead of head.

In the end return dummy.next instead of head.
