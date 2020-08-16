# Interview Prep Notes v2

A second attempt at compiling notes for interview prep for various topics.


### List of additional data structures not part of collections

- Cumulative Array
  - Prefix sum vs 2 pointer - what can/cannot be solved by 2 pointer: https://leetcode.com/problems/subarray-sum-equals-k/discuss/301242/General-summary-of-what-kind-of-problem-can-cannot-solved-by-Two-Pointers
  - Another example is [Shortest Subarray with Sum at Least K](https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k/) which cannot be solved with 2 pointers although it matches the pattern. This is because negative elements count as 'removals'

- Binary search: https://leetcode.com/discuss/general-discussion/786126/python-powerful-ultimate-binary-search-template-solved-many-problems
- Disjoint Set
- Trie
- Segment Tree and Fenwick Tree

DP patterns
- https://leetcode.com/discuss/general-discussion/662866/dp-for-beginners-problems-patterns-sample-solutions
- https://xueyuechuan.me/2018/12/04/Dynamic-Programming-State-Machine/
- https://www.geeksforgeeks.org/partition-problem-dp-18/


Binary Search
- https://leetcode.com/discuss/general-discussion/691825/binary-search-for-beginners-problems-patterns-sample-solutions
- https://www.youtube.com/watch?v=GU7DpgHINWQ&feature=emb_title

Topics
- https://github.com/xiaoylu/leetcode_category

## Learning resources:

- Math for CP: https://codeforces.com/blog/entry/77137
- Bridges and articulation points: https://codeforces.com/blog/entry/68138
  - Note: there is a much better explanation by algorithms live on this
- KMP: https://www.youtube.com/watch?v=y2b94AxPlF8, https://www.youtube.com/watch?v=dyyeSKnBOjc
- Manacher's Algorithm: https://www.youtube.com/watch?v=SV1ZaKCozS4


## Todo:

- Is there a link between dp involving preprocessing input vs dp derived through recurrence?
  - Examine recurrence of buy/sell stock problems and compare it vs preprocessing input structure. Link below:
  - https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/discuss/108870/Most-consistent-ways-of-dealing-with-the-series-of-stock-problems
