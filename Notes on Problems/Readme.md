
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
Crappy problem. Just a bunch of edge cases.

#### 9. Palindrome Number
Return false for negative integer. Reverse the integer storing val in a long by doing `sum = sum*10 + x%10; x = x/10`. If sum is more than max int return false else return `(int)sum == x`.

#### 10. Regular Expression Matching 
