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

|                  |        BST (*balanced*)         |     Binary Search     |
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
bool is BST(Node* p, int min_v, int max_v);
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


If given a key (may or may not actually exist in the BST)
```C++
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

### Insert a key on a BST: Algorithm
Where should we find the right spot to insert a key $x$ on a tree??
Ensure the BST property holds after insertion.

- Follow path to the inserted key, if this key is NULL place in that position

``` C++
// Iterative
void BST::insert(int newKey) {
	Node* curr = root;
	Node* parent = NULL;
	while(curr && curr->key != newKey) {
		if(newkey > curr->key) curr = curr->right;
		if(newkey < curr->key) curr = curr->left;
	}
	// otherwise do not create (only unique keys)
	if (curr) {
		std::cout << "This key already exists." << '\n';
		return;
	}
	Node* p = new (nothrow) Node; // new version of C++ will throw exception instead of null pointer
	assert(p); // to check that 
	p->key = x;
	p->left = p->right = NULL;
	// case: where root is empty
	if(!parent) root = p;
	// make a new node for each corrisponding case
	else if (p->key < parent->key)  {
		parent->left = p;
	}
	else {
		parent->right = p;
	}
}
```

```C++
// Recursive, will require us to have helper function
private:
// remember we want to keep the original root
void BST::insert_helper(Node& p, int newKey) {
	// to search for placement
	if(!p) {
		if(newKey == p->key) {
			std::cout << "This node already exists." << '\n';
		}
		if(newKey > root->key) return insert_helper(root->right, newKey);
		if(newKey < root->key) return insert_helper(root->left, newKey);
	}
	
	Node* p = new (nothrow) Node; // new version of C++ will throw exception instead of null pointer
	assert(p); // to check that 
	p->key = x;
	p->left = p->right = NULL;
	// case: where root is empty
	if(!parent) root = p;
	// make a new node for each corrisponding case
	else if (p->key < parent->key)  {
		parent->left = p;
	}
	else {
		parent->right = p;
	}
	
}
public:
void BST::insert_helper(int newKey) {
	Node* p = root;
	insert_helper(root, newKey);
	return;
}
```
In class version:
```C++
void BST::recurs_insert_helper(BST::Node& p, int x) {
// base case
	if (!p) {
		Node* q = new (nothrow) Node;
		assert(q);
		q->key = x;
		q->left = q->right = NULL;
		p = q;
		return;
	}
	if (p->key == x) return;
	// recursive step
	if (x < p->key)
		recurs_insert_helper(p->left, x);
	else 
		recurs_insert_helper(p->right, x);
}
public:
void BST::recurs_insert() {
	recurs_insert_helper(root, x);
}
```

### Delete a key
(remember corner case where the the node to be delete is the root)
Case1: $x$ has no children
- Easiest (deallocate memory)
Case2: $x$ has one child
- Also easy (grandparent adopts grandchild)
Case3: $x$ has two children
- Complicated (swap $x$ with either the predecessor or successor)
	- This way we keep the BST properties
Case3 can turn into case2 or case1, so start with case3
```C++
bool BST::remove(int x) {
	BST::Node* parent = NULL;
	BST::Node* curr = root;
	while (curr && curr->key != x) {
		parent = curr;
		(x < curr->key) ? curr = curr->left
			: curr = curr->right;
	}
	if (!curr) return false;
	if (curr->left && curr->right) { // case 3
		parent = curr;
		BST::Node* succ = curr->right;
		while (succ->left) {
			parent = succ;
			succ = succ->left;
		}
		curr->key = succ->key;
		curr = succ;
	}
	BST::Node* subtree = (curr->left ? curr->left : curr->right);
	if (!parent)
		root = subtree;
	else {
		if (parent->left == curr)
			parent->left = subtree;
		else parent->right = subtree;
	}
	delete curr;
	return true;
}
```

The issue with BST is that it is expensive to keep balanced.
- Too strict
Red-black trees (still a BST) solve this issue, because it does not need to stay perfectly balanced
- STL `set` is a BST 

### In class Exercises

https://leetcode.com/problems/convert-bst-to-greater-tree/?envType=problem-list-v2&envId=binary-search-tree

```C++
int BST::problem_helper(Node* p, int carry) {
	if (!p) return 0;
	// when finding rightmost carry will remain 0
	int s1 = problem_helper(p->right, carry);
	int s2 = problem_helper(p->left, carry+p->key+s1);
	int sum = s1 + s2 + p->key;
	p->key += s1 + carry;
	return sum;
}
```
--- 
https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/?envType=problem-list-v2&envId=binary-search-tree
```C++
BST::Node* problem(int A[], int lo, int hi) {
	// base case
	if(lo > hi) return nullptr;
	// recursive step
	int mid = lo+((hi-lo)/2);
	Node* p = new Node(A[mid], NULL, NULL);
	assert(p);
	p->left = problem(A, lo, mid-1);
	p->right = problem(A, mid+1, hi);
	return p;
}

// outside we can run
Node* root = problem(A, 0, n-1);
```

https://leetcode.com/problems/minimum-distance-between-bst-nodes/description/?envType=problem-list-v2&envId=binary-search-tree

```C++
// We can use inorder traversal
int BST::problem(BST::Node* p, int& pred, int& rank) {
	if(!p) return INT_MAX; // then distance infinity
	// left subtree
	int d1 = problem(p->left, pred, rank);
	// if you are not the first element
	if (rank > 0)
		d1 = min(d1, p->key - pred);
	pred = p->key;
	rank++;
	// right subtree
	int d2 = problem(p->right, pred, rank);
	return min(d1, d2);
}
// then we can run
int prev, rank = 0;
int ans = problem(root, prev, rank);
```
