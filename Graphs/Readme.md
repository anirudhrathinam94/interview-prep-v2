
## BFS and Shortest Paths

**BFS**

It differs from DFS in that it is often used to solve shortest path problems on **unweighted graph**. We do the following to solve a bfs problem.

- Initialize a queue and a boolean visited array. Insert start node in the queue and mark `visited[start] = true`
- Initialize a null array parent if needed - this helps us reconstruct the shortest path
- While the queue is not empty do the following
  - dequeue the queue. Let's call this element node. Get all the neighbours of node.
  - for all the neighbours, if it is unvisited mark it as visited, enqueue it and set `parent[neighbour] = node`.
- Return the parent array if needed.

**Shortest Paths**

To keep track of the shortest path use an array/map called dist and update it as the program does bfs. This can also serve as the visited array so instead of having a boolean array for visited, have an int array of distances.

- Set `dist[start] = 0` and begin bfs.
- When exploring neighbours if neighbour is unvisited or `dist[neighbour] != null`, enqueue it, set `parent[neighbour] = node` and set `dist[neighbour] = dist[node+1]`

**Practice problems for revision**

- [Word Ladder](https://leetcode.com/problems/word-ladder/)
- [Jump Game 4](https://leetcode.com/problems/jump-game-iv/)

--------

## Topological Sort and Cycle Detection in a DAG

Topological sort involves ordering a directed graph such that each node in the sorted array appears before every other node it points to. Only graphs that are both **directed** and **acyclic** can be topologically sorted.

**Problem Types**

If we want to find how to order a set of entities, topological sort can be considered.

**Cycle Detection in a DAG**

To detect a cycle in a DAG do the following:

```
1. Do a depth first traversal on the graph recording every node in the DFS stack
2. If we try to visit a node that is in the DFS stack, it means there is a cycle.
3. This is the same intuition behind Tarjan's algorithm.
```

**Topological Sort**

The pattern for topsort is as follows:

- Build the graph
- Initialize an index value set to 0 and a result array. The idea is to fill `result[index]` with values in sorted order.
  - An index value of -1 indicates that we have encountered a cycle in the graph.
- Iterate over all nodes of the graph. If a node is unvisited, do a dfs on that node to fill values in the result array.
- In the dfs, our base cases are as follows:
  - If we try to visit a node that is in the stack or if the index = -1 there is a cycle. Return -1
  - If we try to visit a node that has already been visited, we dont need to process it. Return index
- Else we do the following:
  - Mark the current node as visited and add it to set of nodes in the stack
  - For all children of the node we are processing recursively call the dfs function which will fill the result array.
  - If the index is -1, that means a cycle was detected in the previous recursive call so return -1. Otherwise continue.
  - Add the current node to `result[index]` and remove it from set of nodes in the stack
  - Return `index + 1` indicating that `result[index]` has been filled and the next value to fill must be `result[index+1]`

**Practice problems for revision**

- [Course Schedule 2](https://leetcode.com/problems/course-schedule-ii)
- [Alien Dictionary](https://leetcode.com/problems/alien-dictionary)

----------------

# Problems

## BFS and Shortest Paths

**1. Word Ladder**

The problem can be found on leetcode [here](https://leetcode.com/problems/word-ladder/). The code is as follows:

```
class Solution {
    Map<String, List<String>> graph =  new HashMap<>();
    
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        if(beginWord.equals(endWord))
            return 1;
        wordList.add(beginWord);
        buildGraph(wordList);
        return dfs(beginWord, endWord);
    }
    
    private int dfs(String beginWord, String endWord) {
        Queue<String> queue = new LinkedList<>();
        Map<String, Integer> dist = new HashMap<>();
        queue.add(beginWord);
        dist.put(beginWord, 1);
        
        while(!queue.isEmpty()) {
            String node = queue.remove();
            for(String neighbour: graph.get(node)) {
                if(!dist.containsKey(neighbour)) {
                    queue.add(neighbour);
                    dist.put(neighbour, dist.get(node)+1);
                    if(neighbour.equals(endWord))
                        return dist.get(neighbour);
                }
            }
        }
        return 0;
    }
    
    private void buildGraph(List<String> wordList) {
        for(String word1: wordList) {
            if(!graph.containsKey(word1))
                graph.put(word1, new ArrayList<>());
            for(String word2: wordList) {
                if(!word1.equals(word2) && isEdge(word1, word2))
                    graph.get(word1).add(word2);
            }
        }
    }
    
    private boolean isEdge(String word1, String word2) {
        int count = 0;
        for(int i=0; i<word1.length(); i++) {
            if(word1.charAt(i) != word2.charAt(i))
                count++;
            if(count > 1)
                return false;
        }
        return true;
    }
}
```

The complexities are as follows:

- Time: 
- Space: 

---------------

**Jump Game 4**

The problem can be found on leetcode [here](https://leetcode.com/problems/jump-game-iv/). The code is as follows:

```
class Solution {
    
    Map<Integer, List<Integer>> sameValues = new HashMap<>();
    
    public int minJumps(int[] arr) {
        int pre = -1;
        for(int i=0; i<arr.length; i++) {
            if(!sameValues.containsKey(arr[i])) {
                sameValues.put(arr[i], new ArrayList<>());
                pre = i;
            }
            // we do some pruning here if we have [7,7,7] we dont need to visit the middle 7                  
            if(i == pre || i == arr.length-1 || arr[i] != arr[i+1])
                sameValues.get(arr[i]).add(i);
        }
        return bfs(arr);
    }
    
    private int bfs(int[] arr) {
        int[] dist = new int[arr.length];
        Arrays.fill(dist, -1);
        Queue<Integer> queue = new LinkedList<>();
        dist[0] = 0;
        queue.add(0);
        int n = arr.length;
        while(!queue.isEmpty()) {
            int i = queue.remove();
            int cost = dist[i];
            if(i != 0 && dist[i-1] == -1) {
                queue.add(i-1);
                dist[i-1] = cost+1;
            }
            if(i != n-1 && dist[i+1] == -1) {
                queue.add(i+1);
                dist[i+1] = cost+1;
            }
            for(int neighbour: sameValues.get(arr[i])) {
                if(dist[neighbour] == -1) {
                    queue.add(neighbour);
                    dist[neighbour] = cost+1;
                }
            }
            if(i == n-1)
                return dist[n-1];
        }
        return -1;
    }
}
```

The complexities are as follows:

- Time: 
- Space: 

--------------

## Topological Sort and Cycle Detection in a DAG

**1. Course Schedule 2**

The problem can be found on leetcode [here](https://leetcode.com/problems/course-schedule-ii). The code is as follows:

```
class Solution {
    Map<Integer, Set<Integer>> graph;
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        graph = buildGraph(numCourses, prerequisites);
        return topSort();
    }
    
    private int[] topSort() {
        int[] res = new int[graph.size()];
        boolean[] visited = new boolean[graph.size()];
        boolean[] instack = new boolean[graph.size()];
        int index = 0;
        for(int i=0; i<graph.size(); i++) {
            index = dfs(index, i, res, visited, instack);            
            if(index == -1)     // there is a cycle return empty array
                return new int[0];
        }
        return res;
    }
    
    private int dfs(int index, int i, int[] res, boolean[] visited, boolean[] instack) {
        if(instack[i] || index == -1)
            return -1;        
        if(visited[i])
            return index;
        visited[i] = true;
        instack[i] = true;
        
        for(int child: graph.get(i))
            index = dfs(index, child, res, visited, instack);
        if(index == -1)
            return -1;   
        res[index] = i;
        instack[i] = false;
        return index+1;
    }
    
    private Map<Integer, Set<Integer>> buildGraph(int n, int[][] prerequisites) {
        Map<Integer, Set<Integer>> map = new HashMap<>();
        for(int i =0; i<n; i++)
            map.put(i, new HashSet<Integer>());
        for(int i=0; i<prerequisites.length; i++) {
            Set<Integer> set = map.get(prerequisites[i][0]);
            set.add(prerequisites[i][1]);
        }
        return map;
    }
}
```

The complexities are as follows:

- Time: O(n) to build the graph where n is prerequisites.length
- Time: O(V + E) for topsort
- Space: O(V * E)

------------

**2. Alien Dictionary**

The problem can be found on leetcode [here](https://leetcode.com/problems/alien-dictionary). The code is as follows:

```
class Solution {
    
    Map<Integer, Set<Integer>> graph = new HashMap<>();
    boolean invalid = false;
    
    public String alienOrder(String[] words) {
        if(words.length == 1) return words[0];
        buildGraph(words);
        if(invalid) return "";
        
        return topSort();
    }
    
    private String topSort() {
        char[] res = new char[graph.size()];
        boolean[] visited = new boolean[26];
        boolean[] instack = new boolean[26];
        int index = 0;
        
        for(int i: graph.keySet()) {
            if(!visited[i])
                index = dfs(index, i, res, visited, instack);
            if(index == -1)     // there is a cycle return empty string
                return "";
        }
        
        return new String(res);
    }
    
    private int dfs(int index, int i, char[] res, boolean[] visited, boolean[] instack) {
        if(instack[i] || index == -1)
            return -1;
        if(visited[i])
            return index;
        visited[i] = true;
        instack[i] = true;
        
        for(int child: graph.get(i))
            index = dfs(index, child, res, visited, instack);
        if(index == -1)
            return -1;
        res[index] = getChar(i);
        instack[i] = false;
        return index+1;
    }
    
    private void buildGraph(String[] words) {
        for(int i=0; i<words.length-1; i++) {
            String w1 = words[i];
            String w2 = words[i+1];
            
            for(int j=0; j<w1.length(); j++)
                if(!graph.containsKey( getNum(w1.charAt(j)) ))
                    graph.put(getNum(w1.charAt(j)), new HashSet<>());
            
            for(int j=0; j<w2.length(); j++)
                if(!graph.containsKey( getNum(w2.charAt(j)) ))
                    graph.put(getNum(w2.charAt(j)), new HashSet<>());
            
            for(int j=0; j<Math.min(w1.length(), w2.length()); j++) {
                if(w1.charAt(j) != w2.charAt(j)) {
                    graph.get(getNum(w2.charAt(j))).add(getNum(w1.charAt(j)));
                    break;
                }
            }
            
            if(w2.length() < w1.length() && w2.equals(w1.substring(0, w2.length())) ) {
                invalid = true;
                return;
            }
        }
    }
    
    private int getNum(char c) {
        return c - 'a';
    }
    private char getChar(int i) {
        return (char) (i+'a');
    }
}
```

The complexities are as follows:

- Time: O(n * l) to build the graph where n is number of words and l is length of longest word
- Time: O(V + E) for topsort
- Space: O(V * E)
