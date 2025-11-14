## Checklist
### Time Efficiency Analysis
- [x] Big-O Notation
- [x] Find $T(n)$ for a code segment

### Trees, Binary Trees, and Complete Binary Trees
- [x] Tree terminologies: leaf, root, parent, child, height, depth, path, etc.
- [x] Tree representations: array-based and linked-list based.
- [x] Tree traversal: in-order, preorder, and post-order

### Binary Search Trees (BST)
- [x] BST property
- [x] All basic operations
	- [x] insert
	- [x] remove
- [x] $T(n) = O(logn)$ for many operations if the tree is balanced



```C++
void leaf_helper(Node* curr, int& sum) const {
	if (!curr) return;
	if (!(curr->left) && !(curr->right))
		sum = sum + curr->key;
	// Should have no return for recursive functions (since void)
	leaf_helper(curr->left, sum);
	leaf_helper(curr->right, sum);
}
int leafKeySum() const {
	int sum = 0;
	leaf_helper(root, sum);
	return sum;
}

Node* getSuccessor(const int& x) const {
	Node* curr = root;
	Node* parent = NULL;
	while (curr && curr->key != x) {
		if (x < curr->key) {
			parent = curr;
			curr = curr->left;
		} else
			curr = curr->right;
	}	
	if (!parent && !(curr->right)) return NULL;
	if (curr && curr->right) {
		parent = curr->right;
		while (parent->left)
			parent = parent->left;
	}
	return parent; // Should handle case where successor is ancestor
}
```