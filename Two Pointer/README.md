
### Largest Substring or Subsequence that satisfies a given condition

**Pattern**

The pattern is as follows

- Maintain a cache for all visited elements the condition will be validated against this cache. Start with 2 pointers at index 0. 
- Keep increasing fast pointer while continuously storing values in the cache until either end of loop or until condition is violated. 
  - For each new value stored in the cache update the max.
- If condition is violated increment slow pointer removing values in the cache until condition is satisfied again.

**Practice problems for revision**

- [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

-----------------

### Converging pointer problems

Questions that fall under this category are usually in the format: Select 'x' distinct elements from an array/arrays that satisfy a given condition. Note that **this does not cover maximization/minimization problems** those problems can be covered by other patterns like backtracking or dp.

The pattern is as follows:

- **OPTIONAL:** Depending on the problem there may be an optional preprocessing step like sorting the array etc. 
- Initialize a left pointer at start and right pointer at end.
- While left is less than right do the following:
  - Select a[left] and a[right]. Find the value you get by selecting these 2 points. If condition is satisfied return/add to list/whatever.
  - Otherwise increment either left or right in a greedy manner depending on the problem type.

**Practice problems for revision**

- [3Sum](https://leetcode.com/problems/3sum/)
- [Array Sampling](https://github.com/eyarovoi/TechInterviewsMeetup/blob/master/Problem%20Solving%20Workshops/PSW021_2017_03_04/PSW021_2017_03_04.pdf)
- [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

------------

### Smallest Substring or Subsequence that satisfies a given condition (not exactly 2 pointer but I have put it here so I dont forget)

**Practice problems for revision**

- [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
- [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/) uses a similar concept maybe there is a link? (to-do)
