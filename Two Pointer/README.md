
### Largest Substring or Subsequence that satisfies a given condition

**Pattern**

The pattern is as follows

- Maintain a cache for all visited elements the condition will be validated against this cache. Start with 2 pointers at index 0. 
- Keep increasing fast pointer while continuously storing values in the cache until either end of loop or until condition is violated. 
  - For each new value stored in the cache update the max.
- If condition is violated increment slow pointer removing values in the cache until condition is satisfied again.

**Practice problems for revision**

- [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

### Smallest Substring or Subsequence that satisfies a given condition

**Practice problems for revision**

- [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
