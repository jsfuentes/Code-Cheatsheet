# Data Structures

- Hashmap
  - Used for set and easy checking for existence in
  - Constant lookup, no ordering
- Linked list
  - Pretty useless besides fast insertion, so deque
    - Javascript doesnt even have one
- Array
  - Standard in most languages, constant lookup and ordered 
- Tree
  - Show up in DOM, File Systems, and more
  - Binary Search Tree, AVL Trees and Red-Black Trees(self balancing BST)
    - Good for keeping ordering despite rapid insertion and deletion(arrays would require shifts)
    - Efficient range querying
  - Often used in Databases, B-Trees or B+Trees
    - MySQL, PostgreSQL, and many NoSQL databases, use B+Trees for indexing 
- Graph
  - Transportation, social/relationship networks, dependencies
  - Bfs, dfs, prims, Dijkstra
  
- Other Vocab Words: 
  - Dynamic Array, queue, deque(both ends), stack 
  - trie(store strings by tree of characters), heap(BST with smallest value as root, easy priority queue), min-heaps and max-heaps(can be represented in array) 
  - [bloom filter](https://en.wikipedia.org/wiki/Bloom_filter), Ordered Dict(dict for lookup and linked list for order), LRU cache


### How do databases store files?

- 