Recursive data structure

## In class

Trees are everywhere: 
- Directory tree in file systems
- Decision trees in machine learning
- In networking and distributed systems, the tree-like structure makes systems scalable (DNS, internet topology, etc.)

proof of induction

### Tree terminology

1) A tree is a connected graph 
	- Every node can be reached from the root by following a single path: *consecutive edges*
2) No cycles
3) n nodes = n+edges (proof by induction)
	 - proof: Each edge connects a node to its parent. Every node except the root has a parent

**Tree depth**
Depth of a node:
- = the length of the path from the root to the node
- = the number of edges on this path
- The root is at depth 0
…
**Tree height**
Height of a node: 
- = longest path from the node to any leaf
- The height of any leaf is 0
Height of a tree:
- = the height of its root
- = max($h_i$) for all nodes $i$ in the tree
Tree height = tree depth

…(proper ancestor)
… (leaf node when no children) ($nStored = 2^{level})$

Vertices and Edges
- A finite set of elements called nodes or vertices
- A finite set of directed edge which connect the nodes (parent→child)
Recursive data structure
- Base case: Empty tree (0 nodes)
- Recursive case: one root node+subtrees
**Tree representation in memory**
Which one of these we use depends on the type of tree: (But usually array is faster)
- Use an array ( or STL vector)
- Use a linked list

**Using an Array to store a Binary Tree** (Often better)
Note: If the tree must be incomplete a linked list may be more optimal
- Number nodes from the root node in a top-down fashion
- On each level, number nodes from left to right
- The number of each node corresponds to the index position in the array
- (Think of folding tree so that it becomes linear)
parent = $i$
left child = $2*i+1$
right child = $2*i+2$
You can infer the parent child relationship
parent = $\frac{i-1}{2}$

**Using a linked list to store binary trees** (Often worse)
Note: If the tree must be incomplete a linked list may be more optimal
```C++
typedef int ElementType;
Struct Node {
	ElementType data;
	Node* left;
	Node* right;
	// Node* parent; // optional(like a doubly linked list)
}
```
Note: from now on we focus on binary tree
**Complete Tree**
*Definition*:
- Each level is completely filled except the bottom level
- Fill nodes from left to right
Incomplete trees will waste memory
If the tree must be incomplete a linked list may be more optimal


**Recursion in tree**
```C++
Struct Node { // binary tree nodes
	int data;
	int height;
	int depth
	Node* left;
	Node* right;
};
// Store each nodes depth w/ recursion (each node will have accurate depth)
void get_depth(Node* root, int depth) {
	if (!root) return 0; // base case
	// recursive step
	root->depth = depth;
	get_depth(root->left, depth+1);
	get_depth(root->right, depth+1);
}

void get_height(Node* root) {
	if (!root) return -1; // base case
	// recursive step
	// get highest height from the each root->left and root->right
	root->height = max(get_height(root->left), get_height(root->right)) + 1;
}
```

**Tree Traversals**
- Visits every node and every edge on a tree
- 3 tree traversals: permutations of traversal orders
	- *Inorder:* Left subtree→Root→Right subtree
	- *Preorder:* Root→Left subtree→Right subtree
	- *Postorder:* Left subtree→Right subtree→Root

**Types of Trees**
- Binary trees
	- BST (Binary Search Tree)
	- Decision trees
	- AVL (Adelson-Velksii and Landis)
	- Others - splay tree, *red/black tree*
- B-trees
	- B+ tree
	- 2-3 tree
- Many others
