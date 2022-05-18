# Trees
**Note:** examples done in java. Notes are written while reading through "Cracking the Coding Interview"

- A data structure that is made up of a interconnected nodes that can be of any type (string, bool, etc...)

- Most basic qualifications for a tree
  - has a root node that has zero or more children
  - every child node has zero or more children

- **Leafs** are nodes that have zero children

## Balanced Trees
- Trees in which an **insert** or **find** operation can run within the time constraint of **O(log n)**
- E.g of balanced Trees are **AVL** or  **red-black**

## Binary Trees
- Trees in which each node can only have up to two children.

  ### Binary Search Trees
  - Binary Trees that follow the criteria of "Left Child Node is <= parent node < Right Child Node"
  - 
  ### Complete Binary Trees
  - Trees in which all layers are full expect possible the last, which fills left to right.


  ### Full Binary Trees
  - Type of Binary Tree
  - Trees in which all children have zero or 2 children

  ### Perfect Binary Trees
  - All rows are filled, and all leaf nodes are on the same level.

  ### Binary Tree Traversal
  - There are three types of traversals:
    - In-Order: "Ascending Order" Goes... **Left** -> **Parent** -> **Right**
  ```java
  void inOrderTraversal(TreeNode node) {
    if (node != null) {
      inOrderTraversal(node.left);
      visit(node);
      inOrderTraversal(node.right);
    }
  }
  ```
    - Pre-Order: Goes... **Parent** -> **Left** -> **Right**
   ```java
   void preOrderTraversal(TreeNode node) {
     if (node != null) {
       visit(node);
       preOrderTraversal(node.left);
       preOrderTraversal(node.right);
     }
   }
   ``` 
    - Post-Order: Goes... **Left** -> **Right** -> Parent
    ```java
    void postOrderTraversal(TreeNode node) {
      if (node != null) {
        postOrderTraversal(node.left);
        postOrderTraversal(node.right);
        visit(node);
      }
    }
    ```
  ### Binary Heaps
  - There are two types:
    - min-heaps: Two potential operations. That both take O(log n) time
      - **insert**:
        - You add the new node to the next available spot on the bottom row. (looking left to right)
        - run a check and traverse the tree until the new node finds it's proper place.
      - **Extract Min Element**:
        - You yank the min element. Then you replace it with the maximum element. Then you proceed to traverse the tree until that max element finds it's new place.
        - 
    - max-heaps
  
## Tries (Prefix Trees)
- Is a data structure that can is commonly used for string/name/word lookups. It is an n-ary tree where characters are stored at each node. And either a * or a boolean flag is used to end a pathway.
- Commonly used to store the entire English Language for quick prefix lookups.
- O(K) time. Which is also the same as a hash table.
- Hash tables are usually used for for telling if a word is a valid word. Tries are faster/better at showing if a word is a prefix of another word.

## Graphs
- SUBSUMPTION!!!! All trees are graphs but not all graphs are trees.
- A graph is a collection of nodes (vertices) that may or may not be connected by edges
- **Important** Not all nodes may be accessible from one origin/root node (start node).
- Two possible types of edges:
  - **directed**: "One-Way" there is only one connected (relationship) between the two nodes
  - **undirected**: "Two-Way" there is two connections between the two nodes.

- A Connected Graph is a graph in which all the nodes are connected

- An **Acyclical Graph** is a graph that does not have cycles.

- In Programming there are two possible ways to represent (Code) a graph
  - **Adjacency List**
    - The most common way. In which every vertex (node) stores a list of adjacent vertices. 
    - The Graph class below is sed because unlike a tree not all nodes are not necessarily accessible through a root node.
    - Ususally Adjacency lists are represented with a single class however you can also use a hash table, a list, dict, arraylists, etc..
    - e.g
```java
class Graph {
  public Node[] nodes;
}

class Node {
  public String name;
  public Node[] children;
}
```
  - **Adjacency Matrixes**
    - A matrix using either boolean values or 0's and 1's to represent connections between vertices.
    - In an undirected graph the adjacency matrix will be symmetric. In a directed graph it will not (necessarily be) 
    - The same search algorithms (breadth-first, etc) will work on either List or martixes however it's important to note that matrixes are usually less efficient.

## Graph Search
  - Two most common ways are:
    - **Depth First Search(DFS):**
      - Start at the root node or a random node. Then work your way down the entire branch before moving on to the next branch.
    - **Breadth First Search(BFS):**
      - Start at the root node or a random node. Then work your way through each neighbor before going down to any children.

  - These are used in differing scenarios
  - DFS is usually used when you want to visit every node in the graph. Both will work just fine though
  - BFS is usually better for finding the shortest path (or just any path) between nodes.

## Depth First Search (DFS)
  - In DFS we go down first then exhuast the neighbors
  - Note that pre-order is a type of DFS and there are other forms
  - the key is that when implementing this alog we need to track what node has already been visited. So that we don't risk and infinite loop.
```java
 void search (Node root){
  if (root == null) return
  visit(root)
  root.visited = true
  for each Node n in root.adjacent:
    if n.visited == false:
      search(n)
 }
```

## Breadth First Search(BFS)
- BFS is a bit less intuitive. The main tripping point is the (false) assumption that BFS is recursive. It's not, instead it uses a queue. 
- An iterative solution involving a queue ususally works best.
```java
void search(Node root):
  Queue queue = new Queue()
  root.marked = true
  queue.enqueue(root) // Add to the end of queue

  while !queue.isEmpty():
    Node r = queue.dequeue() // Remove from the front of the queue
    visit(r)
    for each Node n in r.adjacent:
      if n.marked == false:
        n.marked = true
        queue.enqueue(n)
```


## Bidirectional Search
- is used to find the shortest path between a source and destination node. 
- essentially runs two BFS's. **One from each node**




