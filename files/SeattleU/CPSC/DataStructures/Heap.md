#DataStructures 
### Heap Definition

**Heap:** A complete binary tree with the *heap-order property*.

Remember: Complete binary tree inserts from left to right on the tree.
#### Heap Order Property
|      Heap Type       | Heap-Order Property         |  Max Element   |  Min Element   |
| :------------------: | --------------------------- | :------------: | :------------: |
| **Maxheap**(default) | parent key $\geq$ child key |      root      | some leaf node |
|     **Minheap**      | child key $\geq$ parent key | some leaf node |      root      |
#### Representation of Heap
Number node starting at root in left-traversal, left→right order:
![[image-47.png|373x273]]
- Children of node $k$ are nodes $2k+1$ and $2k+2$
- Parent of node $k$ is node $(k-1)/2$

A heap can be stored in an array $b$ (or a STL vector) in the numbering order:
![[image-48.png|310x130]]
- Children of $b[k]$ are $b[2k+1]$ and $b[2k+2]$
- Parent of $b[k]$ is $b[(k-1)/2]$

### Basic Operations

|        Operation         |                                $T(n)$                                 |
| :----------------------: | :-------------------------------------------------------------------: |
|        **Insert**        |                              $O(\log n)$                              |
|     **Remove root**      |                              $O(\log n)$                              |
|        **Search**        |                                $O(n)$                                 |
| **Remove (any element)** | $O(\log n)$ or $O(n)$, depends on whether a search is required or not |

#### Finding Height of Heap with $n$ Elements
A heap storing $n$ keys has height of $\lceil \log n \rceil$.

Proof: (Complete Binary Tree Property)
- let $h$ be the height of a heap storing $n$ keys
- Since there are $2^i$ keys at depth $i = 0, …,h-1$ and at least one key at depth $h$, we have $n \geq 1 + 2 + 4 + … + 2^{h-1} + 1$
- Thus, $n \geq 2^h$, i.e., $h \leq \log n$
![[image-49.png]]

#### Insertion
For Simplicity this will be shown for Maxheap.
1) Place the new item $x$ at the end of the array and increase the heap size.
	- Satisfy the complete tree property
2) Percolate up (bubble up) until either $x \geq$ parent or or $x$ is the new root.
	- Satisfy the heap-order property
$T(n) = O( \log n)$
![[Heap_Insertion_EX_Extracted.pdf]]
#### Delete root
1) Swap the root and last element, then delete last element.
	- Satisfy the complete tree property
	- Now semi-heap because only the root does not satisfy the heap property
2) Percolate down from the root until either heap-order property holds or it is a leaf
	- Satisfy heap order property
$T(n) = O( \log n)$
![[Heap_Delete_EX_Extracted.pdf]]

#### Delete Any Element
If the element to be deleted is the root: $O(\log n)$
Otherwise, this process is a lot more complicated. A simple approach would have $T(n) = O(n)$.
- This is because there is no guarantee of the element to be deleted is on the left or right subtrees. So we would have to parse the whole tree until we find it.

### Basic Operations - Implementation

**heap.h**
```C++
// File: heap.h

const typedef int ElementType;
const int SIZE = 1000;
class Heap {
private:
	ElementType a[SIZE];
	int count;
	void percolate_up(int pos);
	void percolate_down(int pos);
public:
	Heap();
	~Heap();
	bool insert(ElementType x);
	bool del_max();
}
```

**heap.cpp**
```C++
// File: heap.cpp

bool Heap::insert(ElementType x) {
	if (size + 1 == SIZE) // Do not overgrow heap
		return false;
	a[size++] = x; // add at the end of heap
	percolate_up(size-1); // for heap-order property
	return true;
}
void Heap::percolate_up(int pos) {
	while (pos > 0 && a[pos] > a[(pos-1)/2]) {
		swap(a[pos], a[(pos-1)/2]);
		pos = (pos-1)/2;
	}
}
bool Heap::del_max() {
	if (!count) return false;
	swap(a[0], a[--count]);
	percolate_down(0);
}
void Heap::percolate_down(int pos) {
	while (pos*2+1 < count) {
		int c = pos*2 + 1;
		if (c+1 < count && a[c+1] > a[c])
			c++;
		if (a[c] <= a[pos])
			break;
		swap(a[pos], a[c]);
		pos = c;
	}
}

```