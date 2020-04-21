
## Language Specifics

### Priority Queues

Entries are sorted based on natural ordering of the keys. If we do:

```
PriorityQueue<Integer> pq = new PriorityQueue<>();
for(int i=4; i>=0; i--)
    pq.add(i);
```

The order is `[0, 1, 2, 3, 4]`

### TreeMaps

Entries are sorted based on natural ordering of the keys. If we do:

```
Map<Integer, Integer> map = new TreeMap<>();
for(int i=4; i>=0; i--)
    map.put(i, -1*i);
```

The output is `{0=0, 1=-1, 2=-2, 3=-3, 4=-4}`

### Comparator

Is of a given type. Overrides a method that compares 2 values of that type. Let's assume we compare values (a,b).

- If we return negative value, a is sorted before b
- If we return 0 then they are sorted in any order
- If we return positive value, b is sorted before a

The code is as follows:

```
Comparator<Integer> c = new Comparator<Integer>() {
  @Override
  public int compare(Integer a, Integer b) {
    return b-a;
  }
};
```

If we pass this comparator as a param to the treemap above the output changes to `{4=-4, 3=-3, 2=-2, 1=-1, 0=0}`
