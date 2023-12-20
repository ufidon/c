__Data structures__

_chtp9e ch12_

Basic data structures
---
- _Linked lists_ are collections of data items linked linearly 
  - items can be inserted and deleted anywhere in a linked list
- _Stacks_ are _first-in last-out (FILO)_ linear data structures
  - items can only be inserted and deleted at one end, the _top_
- _Queues_ are _first-in first-out (FIFO)_ linear data structures
  - You can insert only at the queue’s back and delete only from its front
  - The back and front are known as the queue’s tail and head
- _Binary trees_ facilitate 
  - high-speed searching and sorting of data 
  - eliminating duplicate data items 
  - compiling expressions into machine language


Self-referential structures
---
```c
struct node{
  int data;
  struct node *next;
}
```

📝 Practice: implementing data structures
---
- [linked list](../chtp9ecode/ch12/fig12_01.c)
- [stack](../chtp9ecode/ch12/fig12_02.c)
- [queue](../chtp9ecode/ch12/fig12_03.c)
- [tree](../chtp9ecode/ch12/fig12_04.c)