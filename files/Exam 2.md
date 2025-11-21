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

```C++
for (int i = 1; i <= n; i++) {
	for (int k = 1; k <= i; k++) {
		sum = k*k;
	}
}
```
ANSWER HERE IS WRONG
$$\begin{align}
\sum_{i=1}^{n}\sum_{k=1}^{i}1 = \sum_{i=1}^{n}n = n*n = n^2 \\
\text{Therefore, } T(n) = O(n^2); \\
\sum_{k=1}^{i}1 = n \text{, because $i$ occurs $n$ times}
\end{align}$$
