
## Dynamic Programming Patterns

DP revolves around optimizing recurrences. I have categorized DP problems based on how these recurrences are solved.

### Pattern 1: Recursion with known solution state

In this pattern we know the state that holds the answer to the problem. For example:

- [Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/): Here we calculate the min path sum from grid[0][0] to grid[m][n]. By definition the result is stored in f(0,0).
- [Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/): Here we check if s1 starting at character index i matches s2 starting at character index j. Hence it is obvious that the answer will be stored in f(0,0).

So in this pattern we are naturally working towards a **globally optimal** solution that will be stored in the goal state.

### Pattern 2: Recursion with unknown solution state

In this pattern, the goal state is unknown and any of the states could hold the optimal answer. We calculate the **locally optimal** state for every possible state and get the best of the local optimums. For example:

- [Longest Valid Parentheses](https://leetcode.com/problems/longest-valid-parentheses/): Here we calculate the longest parantheses such thay for f(i) the opening paranthesis lies at index i.
  - so if we have `(()(()()` then `f(0) = 0`, `f(1) = 2`, `f(2) = 0`, `f(3) = 0`, `f(4) = 4`, `f(5) = 0`, `f(6) = 2`, `f(7) = 0`
  - from the program's point of view, we dont know which i in f(i) holds the solution state as this can change based on the input so we iterate over each i value and compute the max.
- [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/): Here we calculate the largest f(i,j) value such that s[i...j] is a palindrome.
  - So if we have `abb` then `f(0,0) = 1`, `f(0,1) = 0`, `f(0,2) = 0`, `f(1,1) = 1`, `f(1,2) = 2`, `f(2,2) = 1`. Here the solution state is `f(1,2)` but this can change based on the input so we iterate over each state and compute the max.
