# Algorithms and Data Structures

## Data Structures

### Stacks

- Main operations and and their time compelxities:

  - push: add an item to the top of the stack (TOS); *O(1)* since one side
  - pop: remove an item from TOS; *O(1)* since one side
  - peek: read itme at TOS; *O(1)* since one side
  - length/size: no. of elements in the stack
  - search: _search_ - *O(n)*

- Applications:

  - Paranthesis balancing, palindrome, back button of the browser, undo and redo operations

### Sets

  All elments are unique, Order is maintained

- Main operations and their time compelxities:

  - has: a set has a value or not; *O(n)* need verif
  - add: add an item; *O(1)*
  - delete: remove item; *O(1)*
  - size: no. of elements in the set; *O(1)*
  - union: merge two sets; *O(n * k)*
  - intersection: common elements between two sets: *O(n * k)*
  - difference: difference between two sets: *O(n * k)*
  - subset: wether given set is a subset of the given set: *O(n * k)*

- Applications:

  - For figuring out he shortest path while laying cables for telecomm

### Queue

  FIFO list, with all members being assigned the same priority

- Main operations and their time compelxities:

  - enqueue: add an item; *O(1)*
  - dequeue: remove an item from the begining; *O(n)* all indices have to be remapped
  - front: get first item in queue; *O(1)*
  - back: get last item in queue; *O(1)*
  - isEmpty: emptiness check; *O(1)*
  - size: no. of elements in the array: *O(1)*

- Applications:

  - Server responding to multiple requests

### HashTables/Maps

  Key-value pair storing structure

- Main operations and their time compelxities:

  - get: get a value; *O(1)*
  - set: add key-value pair *O(1)*
  - has: containment; *O(1)*
  - remove: *O(1)*
  - size: no. of elements; *O(1)*

- HashTables use hashong fucntions for storing key - value pairs

  - Collisions can occur when doing so
  - Collision mitigation: (divide increment by size of structure being used by the hashing fucntion for storage)
    - Chanining: Store value in a LL, if collision, add the value at the end of LL. The LL may be in an array
    - Open addressing: Find different slot to store item. Multiple addressing algos
      - Linear Probing: Increment (by one) hash till we find empty slot; Causes clustering, values getting stored in nearby slots thereby delaying probing over time; *(hash1(key) + increment) % size*
      - Quadratic Probing: Increment using a qudratic fucntion; slots are too spread out; May end up in an infinite loop; *(hash1(key) + increment^2) % size*
      - Double Hashing: Use two has fucntions; *(hash1(key) + increment  * hash2(key)) % size*

### Tree

  Nodes, edges and leaves. Non linear DS.

- Main operations and their time compelxities:

  - lookup, insert, delete: *O(logn)* BST

- Traversals:

  - Breadth First
    Level order traversal; Visit each level of the tree
  - Depth First
    - Pre-order - Root, Left, Right
    - in-order - left, root, right
    - post-order - right, left, root

- Height of a Tree
    Number of edges from leaf to root
  - *1 + max(height(leftSubTree), height(rightSubTree))*

- Depth of a Tree
    Number of edges from the root to the leaves

- Applications:

  - Hierarchical Data
  - Databases; Indexing
  - AutoCompletion: Chrome, web searches
  - Compilers; ASTs
  - Compression; jpg, mp3
