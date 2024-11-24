# Red-Black Trees
Red Black Trees are a type of balanced binary search tree that use a set of rules to maintain balance, ensuring logarithmic time complexity for operations like insertion, deletion, and searching, regardless of the initial shape of the tree. Red Black Trees are self-balancing, using a simple color-coding scheme to adjust the tree after each modification.

## Properties of Red-Black Trees
1. Node Color: Each node is either red or black.  

2. Root Property: The root of the tree is always black.

3. Red Property: Red nodes cannot have red children (no two consecutive red nodes on any path).

4. Black Property: Every path from a node to its descendant null nodes (leaves) has the same number of black nodes.

5. Leaf Property: All leaves (NIL nodes) are black.

These properties ensure that the longest path from the root to any leaf is no more than twice as long as the shortest path

## Why Red-Black Trees
Most of the BST operations (e.g., search, max, min, insert, delete.. etc) take O(h) time where h is the height of the BST.  

The cost of these operations may become O(n) for a skewed Binary tree. 

If we make sure that the height of the tree remains O(log n) after every insertion and deletion, then we can guarantee an upper bound of O(log n) for all these operations. The height of a Red-Black tree is always O(log n) where n is the number of nodes in the tree. 

## Key Mechanisms for Ensuring Balance
### Black Height Rule
The tree enforces the rule that every path from the root to a null pointer (leaf) must contain the same number of black nodes.  
This rule prevents the tree from becoming too unbalanced, as the maximum height of a Red-Black Tree is at most twice the minimum height.
### Red-Red Rule (No Consecutive Red Nodes)
A red node cannot have a red parent or child.
This limits the number of consecutive red nodes, preventing the formation of long chains of red nodes, which could lead to imbalance.

### Balancing During Insertions
New Nodes Are Red: When a new node is inserted, it is initially colored red. This minimizes the disruption to the black height rule.  
After insertion, violations may occur (e.g., a red-red conflict). These are resolved as follows:  
#### Recoloring:
If the parent and uncle of the newly inserted node are both red, they are recolored black, and the grandparent is recolored red.
This may propagate up the tree, requiring further fixes.
#### Rotations:
If recoloring alone cannot fix the violation (e.g., the uncle is black), rotations (left or right) are used to rearrange nodes and maintain the binary search property.

### Balancing During Deletions
When a node is deleted, it may cause a double black imbalance (a node appears "doubly black" compared to its siblings).
This is resolved as follows:
#### Sibling Cases:
```Case 1: Red Sibling:```   
A rotation and recoloring make the sibling black, effectively redistributing the imbalance.  

```Case 2: Black Sibling with Red Child:```  
A rotation (and potentially recoloring) fixes the double black issue.  

```Case 3: Black Sibling with No Red Child:```  
Recolor the sibling to red, which may push the double black issue up the tree for further resolution.  

```Root Case:```   
If the root is double black, it is simply recolored black.

### Rotations
Rotations are used to adjust the structure of the tree while maintaining the binary search property:

```Left Rotation:``` Promotes a right child to the parent’s position, shifting the parent left.  

```Right Rotation:``` Promotes a left child to the parent’s position, shifting the parent right.

###  Height Constraints
Due to the black height rule and red-red rule:  

The maximum height of a Red-Black Tree with 
𝑛
n nodes is 
2log(𝑛+1) 2log(n+1).  

This guarantees that the tree remains balanced enough to perform operations in logarithmic time.

### Basic Operations on Red-Black Tree:
 #### search
`` Purpose:`` Find a node with a given key.  

``Procedure:``
Traverse the tree like a standard Binary Search Tree (BST): compare the target key with the current node, moving left if smaller and right if larger.  
``Time Complexity:`` 
𝑂
(
log
⁡
𝑛
)
O(logn), as the height of the tree is logarithmic in the number of nodes.
Note: Searching does not modify the tree, so no rebalancing or recoloring is required.

### Insertion
``Purpose:`` Add a new key to the tree.

``Procedure``
Insert the new key into the tree following BST rules (insert as a leaf node).
Color the new node red (to preserve the black height property).
Fix any violations of RBT properties:
If the parent is black, the tree remains valid.
If the parent is red:  
``Case 1:`` Red parent, red uncle:
Recolor the parent and uncle to black, and the grandparent to red.
Repeat the process at the grandparent.  
``Case 2:`` Red parent, black uncle:
Perform rotations and recolor to fix red-red violations.
Continue until all properties are restored.
Time Complexity: 
𝑂
(
log
⁡
𝑛
)
O(logn) (due to height of the tree).

### Deletion
``Purpose:`` Remove a key from the tree.

```Procedure:  ```

Find the node to be deleted using BST rules.
If the node has two children:
Replace it with its in-order successor or predecessor (a node with at most one child).
If the node is red: Simply remove it (no violations occur).  
If the node is black:
This creates a "double black" node (a black deficit).
Fix the black deficit using the following cases:  

``Case 1: Red sibling:``
Rotate and recolor to turn the sibling black.  
``Case 2: Black sibling with red child:``
Perform a rotation and recolor to restore balance.  
``Case 3: Black sibling with no red child:``
Recolor the sibling red and push the black deficit up to the parent.
Repeat until all properties are restored. 

Time Complexity: 𝑂(log𝑛)

### Rotations
Rotations are used during insertion and deletion to maintain the RBT properties.

``Left Rotation: `` 
Promotes the right child of a node to its parent’s position, shifting the parent down to the left.
``Right Rotation:  ``
Promotes the left child of a node to its parent’s position, shifting the parent down to the right.
``Purpose:  ``
Restructure the tree to balance black height and preserve the BST property.

### Traversals
Red-Black Trees support all standard tree traversal methods.
 
``Inorder Traversal:``  

Visits nodes in ascending order of keys.  
``Preorder Traversal:``  
Useful for exporting the structure of the tree.  
``Postorder Traversal:``  
Common for cleanup operations like deleting nodes.


### Minimum and Maximum
``Find Minimum: `` 
Follow the left child pointers from the root until reaching a leaf.  
``Find Maximum:``  
Follow the right child pointers from the root until reaching a leaf.
Time Complexity: ``O(logn).``

## Advantages of Red-Black Trees
### Guaranteed Balanced Height:

The height of a Red-Black Tree is 
O(logn), ensuring efficient operations like insertion, deletion, and search.  
### Efficient Operations:

Search, insertion, and deletion operations are all 
O(logn), making it ideal for dynamic datasets.

### Self-Balancing:

The tree adjusts itself (via rotations and recoloring) during insertions and deletions, maintaining balance without user intervention.

### Widely Used in Practice:

Many libraries (e.g., ``std::map`` and `std::set` in C++) and database systems use Red-Black Trees due to their predictable performan

### Support for Ordered Operations:

Enables operations like finding the minimum, maximum, successor, predecessor, and range queries efficiently.

## Disadvantages of Red-Black Trees
### Complex Implementation:

The insertion and deletion algorithms are more complex than those of simpler data structures like AVL trees or unbalanced BSTs.
### Higher Constant Factors:

Due to recoloring and more complex logic, Red-Black Trees can be slower than AVL trees for certain workloads, especially read-heavy operations.
### Not Perfectly Balanced:

While height-balanced, Red-Black Trees are not as tightly balanced as AVL trees, which can make some operations slightly less efficient.

### Memory Overhead:

Each node requires an additional color bit, increasing memory usage compared to simpler data structures.
### Difficulty in Debugging and Maintenance:

The complexity of the balancing rules (rotations and recoloring) makes Red-Black Trees harder to debug and maintain.

### Suboptimal for Fixed Datasets:

For static data that doesn’t change often, simpler data structures like sorted arrays or AVL trees might be more efficient.