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

**Load Factor**

**Rehashing**
1) Create a new table
2) Migrate all data into the new table
3) Delete the old table