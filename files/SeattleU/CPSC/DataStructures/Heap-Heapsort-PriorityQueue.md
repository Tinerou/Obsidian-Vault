#DataStructures 

## Heap Data structure
**Heap:** A *complete* binary tree with *heap-order-priority*
- Maxheap/heap: parent's key $\geq$ child's key (we can just call heap since it is default)
- Minheap: parent's key $\leq$ child's key

For a complete tree like a heap, array-based is better:
- Number node starting at root in level-traversal in left-right order
- Array must be sorted (ideally in decreasing order)


unlike BST no order among sibling nodes
Max element: Located at the root
Min element: Located at a leaf node

Leaf 
When finding leaf nodes:
#### Heap vs. BST
|                               | Heap         | BST                      |
| ----------------------------- | ------------ | ------------------------ |
| Complete Binary Tree          | yes          | no                       |
| Implementation                | array-basbed | linked-list              |
| Ordering between parent-child | yes          | yes                      |
| Ordering among siblings       | no           | yes                      |
| Max key                       | root         | right-most               |
| Min key                       | one leaf     | left-most                |
| balanced                      | yes          | depends (not by default) |

### Insert an Element:
1) *Append* it to the end of the keys
	- `a[n++] = key`
	- To keep tree complete
2) *Percolate* up to check if the heap-order property is maintained (swap keys)

heap.h
```C++
#ifndef HEAP_H
#define HEAP_H
#include <cassert>
#include <new>

class Heap {
private:
	int* arr_;
	int cap_;
	int n_; // number of elements
public:
	Heap(int sz = 100);
	~Heap();
	Heap(const Heap& h); // copy constructor
	void insert(int key);
	int top() const;
	void pop(); // remove root node
	void altPop(); // Another way of popping
	Heap& operator=(const Heap& right);
	
private:
	void percolate_up(int i); // percolate up from position i
	void percolate_down(int i);
	void remove(int i);
};

#endif
```
heap.cpp
```C++
Heap::Heap(int sz) {
	assert(sz > 0);
	arr = new (nothrow) int[sz];
	assert(arr_);
	n = 0;
	cap_ = sz;
}
Heap::~Heap() {
	if (arr_)
		delete[] arr_;
}
void Heap::insert(int key) {
	if (n+1 > cap_) return;
	arr_[n_++] = key; // append new key
	percolate_up(n_ - 1);
}
void Heap::percolate_up(int i) {
	assert(i >= 0 && i < n_);
	while (i > 0 && arr_[i] > arr_[(i-1)/2]) {
		swap(arr_[i], arr_[(i-1)/2]);
		i = (i-1)/2;
	}
}

void Heap::percolate_down(int i) {
	assert(i >= 0 && i < n_);
	while (i*2 + 1 <n_) {}=
		int child = arr_[i*2+1]
		if(c+1 < n_ && arr_[child] < arr_[child+1])
			child = child+1;
		if (arr_[i] >= arr_[c])
			break;
		swap(arr_[i], arr_[n]);
		i = child;
	}
}

int Heap::top() const {
	assert(n_ > 0);
	return arr_[0];
}

void Heap::pop() {
	if (n_ > 0)
		remove(0);
}

void Heap::altPop() {
	if (n_ > 0) {
		swap(arr_[0], arr[--n]);
		percolate_down(0);
	}
}

Heap::Heap(const Heap& h) {
	arr_ = new (nothrow) int[h.n_];
	assert(arr_);
	n_ = h.n_, cap_ = h.cap;
	for (int i = 0; i < n_; i++)
		arr[i] = h.arr_[i];
}

Heap& Heap::operator=(const Heap& right) {
	if (this == right) return *this;
	if (arr_)
		delete[] arr;
	arr_ = new (nothrow) int[right.n_];
	assert(arr_);
	n_ = right.n_, cap_ = right.cap;
	for (int i = 0; i < n_; i++)
		arr[i] = right.arr_[i];
	return *this;
}
void Heap::remove(int i) {
	if (i < 0 || i >= n_) return;
	// swap it with the last node's key
	arr_[i] = arr[--n_]; // after we get value decrement array
	// determine promotion or demotion
	if (i > 0 && arr_[i] > arr[(i-1)/2]) // if greater than parent
		percolate_up(i);
	else
		percolate_down(i);
}
```

### Delete an Element
**Semi-heap:** both left and right subtrees are heaps.

```C++
void Heap::remove(int i) {
	if (i < 0 || i >= n_) return;
	// swap it with the last node's key
	arr_[i] = arr[--n_]; // after we get value decrement array
	// determine promotion or demotion
	if (i > 0 && arr_[i] > arr[(i-1)/2]) // if greater than parent
		percolate_up(i);
	else
		percolate_down(i);
}
```

```C++
// 1) swap nodes
// Check if we need to percolate up
// 2) If node to be deleted is already leaf just delete

void Heap::remove(int i) {
	if (i > n_) return; // if i does not exist
	int depth = log(n); // ideally round down
	// if the depth is on the last row just remove
	if (log(i) = depth) {
		delete[i] arr_;
	}
	else {
		int temp = arr_[n];
		arr_[n] = arr[i];
		arr_[i] = temp;
		delete[i] arr_; // not sure if deletion here is correct
		// Now we need to check if we need to percolate up or down
		if ()
	}
	int toRemove = heap[n];
	arr_[n] = arr_[i];
}
```

```C++
#include<iostream>
#include"heap.h"

int main() {
	heap h1(2000);
	
	for (int i = 0; i < 1000; i++)
		h1.insert(i*i);
	cout << h1.top() << std::endl;
	h1.pop();
	std::cout << h1.top() << std::endl;
	
	Heap h2(h1), h3;
	h3 = h2;
	
	// sort from array
	// O(n) = nlogn
	int A[500] = {-55, 100, 44, ....};
	Heap x(500);
	for (int i = 0; i < 500; i++)
		x.insert(A[i]);
	for (int i = 499; i >= 0; i--) {
		A[i] = x.top();
		x.pop();
	}
	
	// find ith highest 
	// also just top() pop() i-1 times then get root value
	Heap y(50);
	for (int i = 0; i < 500; i++) {
	
		y.insert(-A[i])); // using min heap
	}
	std::cout << -y.top() << std::endl;
}
```

How do we sort from an array?
the highest value will be the root.

