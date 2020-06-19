### Sliding windows

A sliding window can be thought of as a subarray that runs over an array. The sliding window length can be either fixed or variable.

**Fixed length sliding window (length = 3)**

An example of a fixed length sliding window of size 3 is as follows:

```
[1 2 3 4 5 6]
[1 2 3]
  [2 3 4]
    [3 4 5]
      [4 5 6]
```

**Variable length sliding window**

An example of a variable length sliding window is as follows:

```
[1 2 3 4 5]
[1]
[1 2]
[1 2 3]
[1 2 3 4]
[1 2 3 4 5]
```

------------

### Monotonic Queue

A monotonic queue is a data structure that can be used to find the following:

1. The next greater/smaller element in a list
2. The maximum/minimum value in a sliding window.

The monotonic queue is a `Deque` that contains elements that are either increasing or decreasing. Let us consider a monotonic queue that is **decreasing** for a **variable length** sliding window as described in the previous section.

The idea is as follows:

- Iterate over the array. If the deque is empty or if the current element `a[i]` is smaller than the first element (top) of the deque add it to the deque.
- Otherwise if current element `a[i]` is larger than the top of the deque keep popping the deque until either the top of the deque is larger than `a[i]` or until the deque is empty.

  - Before trying to add `a[i]` the deque contains the sliding window from `0...i-1`. The **maximum value** in the sliding window is the last element in the deque ie `deque.peekLast()`

  - If a[i] pops out any element from the deque it means that a[i] is the **next greater element** of the element it was responsible for popping out.
