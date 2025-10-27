#DataStructures 

Divide and conquer
## In class

```C++
// Recursive
int get_smallest(Node* root) {
	if(!(root->left)) return root->data;
	return get_smallest(root->left);
}
```

```C++
// Iterative
int get_smallest(Node* root) {
	Node* leftmost = root->left;
	while(!(leftmost->left)) {
		leftmost->left;
	}
	return leftmost->data;
}
```

```C++
// Recursive
Node* search(Node* root, int target) {
	if(!root) return NULL;
	if(root->key == target) return root;
	// try with ternary operator
	if(root->key < target) return find_key(root->left, target);
	else(root->key > target) return find_key(root->right, target);
}
```

```C++
// Iterative
Node* search(Node* root, int target) {
	while(!root) {
		if(root->key == target) return root;
		if(root->key < target) root->left;
		else(root->key > target) root->right;
	}
	return NULL;
}
```

In the real world we use variations of binary search trees

### BST vs. Binary Search

|                  |         BST (balanced)          |     Binary Search     |
| ---------------- |:-------------------------------:|:---------------------:|
| Data storage     | A linked list-based binary tree | A sorted array/vector |
| Search $T(n)$    |           $O(\log n)$           |      $O(\log n)$      |
| Insertion $T(n)$ |           $O(\log n)$           |        $O(n)$         |
| Deletion $T(n)$  |           $O(\log n)$           |        $O(n)$         |
### Binary Search Trees
Can support *dynamic set operations*
- Search, min, max, predecessor, successor, insert, delete
Used to build
- Dictionaries
- Priority Queues
Basic operations take time proportional to the *height* of the tree: $O(h)$

Not necessarily a complete tree
- Use a linked data structure of nodes (linked list)
- root(T) points to the root of tree T

#### A C++ Class for BST
```C++
class BST {
private:
	struct Node {
		int key;
		Node* left;
		Node* right;
	};
	Node* root;
public:
	BST();
	~BST();
	...
};
```

*proof by induction*

Naturally in a BST, inorder traversal allows for Nodes to be parsed through "inorder"
12, 18, 24, 26, 27, 28, 56, 190, 200, 213


Find out if a binary tree is a binary search tree:
Solution #1: In order traversal
Solution #2: `bool isBST(Node* root, int& minv, int& maxv)`
`
```C++
bool isBST(Node* root, int& minv, int& maxv) {
	// base case
	if(!root) {
		minv = INT_MIN;
		maxv = INT_MAX;
		return true;
	}
	// recursive step
	// Must handle case where right node is higher than previous
	// but also higher than others in the tree...
	int left_min, left_max, right_min, right_max;
	return isBST(root->left, left_min, left_max)
	bool b = isBST(root->left, left_min, left_max);
	b &= isBST(root->right, right_min, right_max);
	min_v = left_min;
	max_v = right_max;
	return b && p->key > left_max
		&& p->key < right_min;
}
```
```
bool is BST(Node*p, int min_v, int max_v);
if(!p) return true
return isBST)p->left
```

Search on a BST
``` C++
// Iterative search function
bool BST::search(int target) {
	Node* p = root; // So we don't lose the root
	while(p && p->key != target) {
		if(p->key < target) root = root->left;
		else(p->key > target) root = root->right;
	}
	return p != NULL; // If p = !NULL that means the while loop exited on p-<key != target
}
```

```C++
// do we have to use given root for recursive?
private:
bool BST::search_helper(Node* p, int target) {
	if (!p) return false;
	if (p->key == target) return true;
	// Remember you can use ternary operator here
	if (p->key < target) return search_helper(p->left, target);
	if (p->key > target) return search_helper(p->right, target);
}
// Wrap around with public interface
// For encapsulation we don't wan't to expose the real root node
public:
bool BST::search(int target) {
	return search_helper(root, target);
}
```

Find the successor node of p
Case 1: if p→right != NULL
→ The left-most node on its right subtree
Case 2: otherwise
→ The lowest ancestor node whose left-subtree contains p.
Behind the idea of deletion in a BST

```C++
private: // Private because we cannot return node* to user
BST::Node* BST::successor(Node* p) { // specify scope operator BST::Node*
// Assume p != NULL
	//case 1
	if (p->right) {
		p = p->right;
		while(p->left)
			p = p->left;
		return p;
	}
	// case 2
	Node* curr = root;
	// If p is the rightmost node on whole tree successor is NULL
	Node* succ = NULL; 
	while (curr && curr != p) {
		if(p->key < curr->key) {
			succ = curr;
			curr = curr->left;
		} else curr = curr->right
	}
	return succ;
}
```
predecessor is pretty much the same thing

```C++
// If given a key (may or may not actually exist in the BST)
int BST::successor(int key) {
	Node* curr = root;
	int ans;
	while (curr && curr != key) {
		if(key < curr->key){
			ans = curr->key;
			curr = curr->left;
		} else curr = curr->right;
	}
	if (curr && curr->right) {
		curr = curr->right;
		while(curr->left) curr = curr->left;
		ans = curr->key;
	}
	return ans
}
```