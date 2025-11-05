#DataStructures 

Maintenance for a *balanced* BST is not easy,
we can use rotation,

Is $Ologn$ good enough?

Not always, so we want a $O(1)$ time complexity.
The solution to this is **hashing**.

### Why Hashing?

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
	int m; // prime number
	int n; // # of keys
public:
	Lptab() {
		n = 0, m = 7;
		ht = new Entry[m];
		assert(ht);
		for (int i = 0; i < m; i++)
			ht[i].state = EMPTY;
	}
	~Lptab() {
	if (ht)
		delete[] ht;
	}
	bool Empty() const { return !n;}
	bool contains(int val) const;
	void put(int val);
	void remove(int val);
private:
	// hash function
	int hash(int k) {
		return (2*k + 5) % m
	}
	void rehash(int sz);
}
```

lptab.cpp
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
	for (k = hash(val); ht[k].state == EMPTY || ht[k].state == DELETED || ht[k].key == val); k = (k+1)%m);
	if (ht[k].state != USED)
		n++;
	ht[k] = val;
	// rehash
	if ((double)n >= 0.7*m) {
		m 
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