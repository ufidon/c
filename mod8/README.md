__Algorithms__

_chtp9e ch13_


Efficiency of Algorithms: Big O
---
- $O(1)$ - constant run time
- $O(n)$ - linear run time
- $O(n^2)$ - quadratic run time


Selection sort
---
- in each iteration, find the smallest element in the unsorted part and put it in the sorted part
- [implementation](../chtp9ecode/ch13/fig13_01.c)
- efficiency: $O(n^2)$


Insertion sort
---
- in each iteration, insert the first unvisited element into the sorted part
- [implementation](../chtp9ecode/ch13/fig13_02.c)
- efficiency: $O(n^2)$


Merge sort
---
- divide and conquer
  - divide down to each element then merge upward
  - merge sorted sub array
- [implementation](../chtp9ecode/ch13/fig13_03.c)
- efficiency: $O(n\log n)$