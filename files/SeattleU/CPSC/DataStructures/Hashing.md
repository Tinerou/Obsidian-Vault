#DataStructures 

Maintenance for a *balanced* BST is not easy,
we can use rotation,

Is $Ologn$ good enough?

Not always, so we want a $O(1)$ time complexity.
The solution to this is **hashing**.

### Why Hashing?
![[image-9.png]]

|             | **Sorted List** | **Balanced BST** | **Hashing** |
| ----------- | --------------- | ---------------- | ----------- |
| *Insertion* | $O(n)$          | $O(\log n)$      | $O(1)$ avg. |
| *Deletion*  | $O(n)$          | $O(\log n)$      | $O(1)$ avg. |
| *Retrieval* | $O(\log n)$     | $O(\log n)$      | $O(1)$ avg. |
- When hash is not $O(1) it is due to a *collision*

### Hashing Definition
#### Hash function $h$
Maps a `key` from a *large* data space into an `index` of a *smaller* space of a hash table
- Maps keys from a *large* data space to *smaller* integers
	- Constrained by the hash table size
#### Hash Table
- Stores `(key, value)` pairs

#### Two Main Issues:
1) How to find a good hash function?
	- Fast to compute
	- Less collision
	- Less space
2) How to resolve collisions?

### Hash Table: Operations
put(key, value)
delete(key)
get(key)
### Collision
Main issue with hashing

When two different keys have the same hash value.
 - There are different hash functions we will use. Some are faster some are slower, and some have higher or lower probabilities of collision.

Resolution techniques:
1) Separate Chaining (Most popular)
2) Open Addressing
	- Linear Probing
	- Quadratic Probing
	- Double Hashing
Separate Chaining: When collision occurs add to linked list within the table

Linear Probing: When collision occurs move to next open index
- Linearly scan the hash table
- Wrap around if reach end of table
- Deletion is complicated, if something gets deleted you will have to put a "tombstone" in that missing position.
	- Use three different states of a slot:
		- Occupied
		- Occupied but marked as deleted
		- Empty
- Main problem: Primary clustering (consecutively occupied slots)
- To help with the issue we can use *modified* linear probing

Quadratic probing: Must have load factor ($\alpha$) < 0.5
- Issue: If two keys have the same initial position, their probe sequences are the same.
	-  Increases memory but faster than linear probing
	- This is called *secondary clustering*
… 
Double Hashing:

- Issue avoid 0 in secondary hash function



### Hash Functions

#### Uniform Hash Functions
Distributes keys evenly in the hash table
##### Example
If integer keys $k \in [0, X)$, are uniformly distributed, use a hash function:
$$
h(k) = \left\lfloor  \frac{km}{X}  \right\rfloor 
$$
Note: 
- $0 \leq k < X$
- $m$ is hash table size
- $\lfloor  \rfloor \text{ is the floor function}$

#### Division Method (mod operator)

Hash function $h$:
- $h(k)=k \% m$,
- where $m$ is hash table size
Choosing $m$:
- $m$ cannot be power for 2 $(2^n)$ or power of 10 $(10^n)$
- Pick a *prime number* close to a power of 2

#### Multiplication Method
#### Hashing of strings

**Load Factor** $\alpha$:


**Rehashing**
1) Create a new table
2) Migrate all data into the new table
3) Delete the old table

lptab.h
```C++
#ifndef LPTAB_H
#define LPTAB_H
#include <cassert>
class LpTab {
private:
	enum State {EMPTY, USED, DELETED};
	struct Entry {
		int key;
		State state;
	};
	// hashtable
	Entry* ht; // hashtable consists of array of Entries
	int m; // table size (prime number)
	int n; // Number of keys
public:
	Lptab() {
		n = 0, m = 7; // m = starting size
		ht = new Entry[m]; // Initialize Entry array members(hash table)
		assert(ht); // check heap allocation
		// set each member to EMPTY
		for (int i = 0; i < m; i++)
			ht[i].state = EMPTY;
	}
	~Lptab() {
		if (ht) delete[] ht;
	}
	bool empty() const { return !n;}
	bool contains(int val) const;
	void put(int val);
	void remove(int val);
private:
	// hash function
	int hash(int k) {
		return (2*k + 5) % m
	}
	void rehash(int sz); // for simplicity we'll assume we found prime num
};

#endif
```

lptab.cpp (In class)
```C++
#include"lptab.h"
#include<iostream>

bool LpTab::contains(int val) const {
	int key = hash(val);
	// If key is not found in table wrap around until found, or table is empty.
	while (ht[key].state == DELETED || (ht[key].state == USED && val != ht[key].key))
		key = (key+1) % m;
	return !(ht[key].state) == EMPTY;
}

void LpTab::put(int val) {
	for (k = hash(val); ht[k].state == EMPTY || ht[k].state == DELETED || ht[k].key == val); k = (k+1)%m));
	if (ht[k].state != USED)
		n++;
	ht[k] = val;
	// rehash
	if ((double)n >= 0.7*m) {
		rehash(2*m);
	}
}

void LpTab::rehash(int sz) {
	// step 1:
	sz = findPrime(sz); // assume we found prime num closest to sz
	// step 2:
	Entry* newHt = new Entry[sz];
	assert(newHt);
	for (int i = 0; i < sz; i++)
		ht[i].state = EMPTY;
	// step 3: copy keys from older table
	swap(ht, newHt);
	swap(m, sz);
}
```



```C++
bool LpTab::contains(int val) const {
	int key = hash(val);
	int start = key;
	do {
		if (ht[key].state == USED && ht[key] == val) 
			return true;
		if (ht[key] state == EMPTY)
			return false;
		key = (key + 1) % m;
	} while (key != start);
	// If not found and hashtable is full
	return false;
}

void LpTab::put(int val) {
	int k = hash(val);
	int start = k;
	do {
		if (ht[k].state == EMPTY || ht[k].state == DELETED) {
			ht[k].key = val;
			ht[k].state = USED;
			n++; // Update num of keys
			return;
		}
		if (ht[k].state == USED && ht[k].key == val) {
			// key already exists
			std::cout << "Value already exists." << std::endl;
			return;
		}
		k = (k + 1) % m;
	} while (k != start); // though it should never reach this point
	// Rehash at 70% load factor
	if ((double)n >= 0.7 * m)
		rehash(2 * m); // double the size
}

void LpTab::remove(int val) {
	int key = hash(val);
	int start = key;
	do {
		if (ht[key].key == val) {
			ht[key].state = DELETED;
			n--;
			return;
		}
		// If val not found
		if (ht[key].state == EMPTY)
			return;
		key = (key + 1) % m;
	} while (key != start)
}

// rehash is basically constructor of new ht and destructor of old ht
void LpTab::rehash(int size) {
	size = findPrime(size); // assume we have a findPrime() function
	Entry* newHt = new Entry[size];
	assert(newHt); 
	
	// Initialize new table
	for (int i = 0; i < size; i++)
		newHt[i].state = EMPTY;
	
	std::swap(ht, newHt);
	m = size;
	n = 0;
	
	
	delete[] newHt;
}
```


### LpTab (Linear Probing):

#### Design
Data Members:
-  `m`: hash table size
- `n`: Number of keys
- `ht`: hash table
- ``` C++
  Entry {
	  key
	  state (USED | EMPTY | DELETED)
  }
  ```
Public Functions:
1) Constructor: Allocate `ht`, initialization
2) Destructor: Deallocate `ht`
3) empty(): `return !n`
4) contains(int val): Find val (use put())
5) put(int val):
	- if value exists (use contains()),  `return`
	- Otherwise, insert → find open slot
	- rehash() if over 70% load factor
6) remove(int val):
	- if val exists → set to `DELETED`
	- otherwise do nothing
	- rehash() if over 70% load factor
7) rehash (private member function)
- Use swap() to swap tables
**lpTab.h**
```C++
#ifndef LPTAB_H
#define LPTAB_H

class LpTab {
private:
	unsigned int m; // hash table size
	unsigned int n; // # of keys
	enum State {EMPTY, USED, DELETE};
	struct Entry {
		int key;
		State state;
	};
	Entry* ht; // hash table

public:
	LpTab(unsinged int size = 7);
	~LpTab();
	bool Empty() const;
	bool Contains(int k) const;
	void Put(int k);
	void Remove(int k);
	
private:
	unsigned int hash(int k) {
		return 9(k << 1) % m; // 9(k*2) + 5
	}
	void rehash(unsigned int sz);
	int find(int k);
	int next(int pos); // find next open position on hash table
};

#endif
```
**lpTab.cpp**
``` C++
#include<cassert>
#include"lptab.h"

LpTab::LpTab(unsigned int size = 7) : n(0), m(sz) {
	ht = new Entry[m];
	assert(ht);
	for (int i = 0; i < m; i++) {
		ht[i].state = EMPTY;
	}
}

LpTab::LpTab() {
	if (ht)
		[delete[] ht;
}

bool LpTab::find(int k) const {
	for (int i = hash(k); !(ht[i].state == EMPTY || (ht[i].state==USED && ht[i].key == k)); )
		k = (k+1) % m; // should we put this in for loop?
	return ht[i].state == USED ? i : -1;
}

// Used to find the next position
int LpTab::next(int pos) {
	while (ht[pos].state == USED)
		pos = (pos+1)%m;
	return pos;
}

bool LpTab::Contains(int k) const {
	return find(hash(k)) != -1;
}

void LpTab::Put(int k) {
	if (Contain(k))
		return;
	int pos = next(hash(k));
	ht[pos].key = k;
	ht[pos].state = USED;
	n++;
	
	// Check load factor
	if ((double)n >= m*0.7) // often avoid hard coding load factor
		rehash(m<<1); // rehash with m*2
}

void LpTab::Remove(int k) {
	int pos = find(k);
	if (pos == -1) return;
	ht[pos].state = DELETED;
	n--;
	
	// Check load factor
	// since we're removing check if we need to reduce hash table
	if ((double)n >= m*0.25) 
		rehash(m>>1); // rehash with m/2
}

void LpTab::rehash(unsigned int sz) {
	int newSize = fitting(sz); // fitting() finds closes prime number to sz
	// step 1: memory allocation
	Entry* newHt = new Entry[newSize];
	assert(newSize);
	for (int i = 0; i < newSize; i++)
		newHt[i].state = EMPTY;
	// step 2: Swap table
	std::swap(ht, newHt);
	int oldM = m;
	m = newSize;
	n = 0; 
	// step 3: Key migration
	// We aviod using Put() due to risk of rehashing again (May not be best implementation)
	for (int i = 0; i < oldM; i++) {
		if (newHt[i].state == USED) {
			int pos = next(hash(newHt[i].key));
			ht[pos].key = newHt[i].key;
			ht[pos].state = USED;
			n++;
		}
	}
	// step 4: deallocation
	delete[] newHt;
	
}
```


Try doing the class problems while using base class before using different hashing techniques.


