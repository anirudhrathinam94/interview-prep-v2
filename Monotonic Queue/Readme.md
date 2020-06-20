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
3. Number of adjacent elements with at least value of current element

The monotonic queue is a `Deque` that contains elements that are either increasing or decreasing. Let us consider a monotonic queue that is **decreasing** for a **variable length** sliding window as described in the previous section.

The idea is as follows:

- Iterate over the array. If the deque is empty or if the current element `a[i]` is smaller than the first element (top) of the deque add it to the deque.
- Otherwise if current element `a[i]` is larger than the top of the deque keep popping the deque until either the top of the deque is larger than `a[i]` or until the deque is empty.

  - Before trying to add `a[i]` the deque contains the sliding window from `0...i-1`. The **maximum value** in the sliding window is the last element in the deque ie `deque.peekLast()`

  - If a[i] pops out any element from the deque it means that a[i] is the **next greater element** of the element it was responsible for popping out.
  

---------------


### Example problems for the two use cases

**Example 1:** [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)

Here we need to find the next greater element for every element and calculate the difference `next_greater(i) - i`. The program to do this is below:

    public int[] dailyTemperatures(int[] a) {
        Deque<Integer> deque = new LinkedList<>();
        int[] res = new int[a.length];
        
        for(int i=0; i<a.length; i++) {
            while(!deque.isEmpty() && a[deque.peekFirst()] < a[i]) {
                int current = deque.removeFirst();
                res[current] = i-current;
            }
            deque.addFirst(i);
        }
        return res;
    } 
    
**Example 2:** [Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)

Here we need to find the maximum of a fixed size sliding window. To remove older elements of the window from the deque we only need to check if the older element is at deque.peekLast(). The program is below.

    public int[] maxSlidingWindow(int[] a, int k) {
        int[] res = new int[a.length-k+1];
        Deque<Integer> deque = new LinkedList<>();
        int resIndex = 0;
        
        // Fill the deque with the contents of sliding window initial
        for(int i=0; i<k; i++) {
            while(!deque.isEmpty() && a[deque.peekFirst()] < a[i]) {
                deque.removeFirst();
            }
            deque.addFirst(i);
        }
        
        res[resIndex] = a[deque.peekLast()];
        resIndex++;
        
        // Slide the window
        for(int i=k; i<a.length; i++) {
            
            // remove leftmost element if it is in deque
            if(a[deque.peekLast()] == a[i-k]) {
                deque.removeLast();
            }
            
            while(!deque.isEmpty() && a[deque.peekFirst()] < a[i]) {
                deque.removeFirst();
            }
            deque.addFirst(i);
            
            res[resIndex] = a[deque.peekLast()];
            resIndex++;
        }
        
        return res;
    }
