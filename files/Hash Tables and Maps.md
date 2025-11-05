
### Maps

A **map** stores key-value pairs $(k, v)$, which are called *entries*, where $k$ is the key and $v$ is its corresponding value.
- The map ADT requires that each key be unique
To implement this concept, we define a class that stores two objects in its first and second member variables, respectively, and provides functions to access and update these variables
```C++
class Entry {                                     // a (key, value) pair
public:                                           // public functions
  Entry(const std::string& k = std::string(), const int& v = 0)       // constructor
    : key(k), value(v) { }
  const std::string& key() const { return key;}            // get key
  const int& value() const { return value;}        // get value
  void setKey(const std::string& k) { key = k;}            // set key
  void setValue(const int& v) { value = v;}        // set value
private:                                          // private data
  std::string key;                              // key (string type)
  int value;                                    // value (int type)
};
```

Informal C++ Map interface (not a complete classs
``` C++
class Map {                                 // map interface
public:
  class Entry;                              // a (key,value) pair
  class Iterator;                           // an iterator (and position)

  int size() const;                         // number of entries in the map
  bool empty() const;                       // is the map empty?
  Iterator find(const std::string& k) const; // find entry with key k
  Iterator put(const std::string& k, const int& v); // insert/replace pair (k,v)
  void erase(const std::string& k)          // remove entry with key k
     throw (NonexistentElement);
  void erase(const Iterator& p);            // erase entry at p
  Iterator begin();                         // iterator to first entry
  Iterator end();                           // iterator to end entry
};

// Entry class without templates
class Map::Entry {                                     // a (key, value) pair
public:                                           // public functions
  Entry(const std::string& k = std::string(), const int& v = 0)       // constructor
    : key(k), value(v) { }
  const std::string& getKey() const { return key;}            // get key
  const int& getValue() const { return value;}        // get value
  void setKey(const std::string& k) { key = k;}            // set key
  void setValue(const int& v) { value = v;}        // set value
private:                                          // private data
  std::string key;                               // key
  int value;                                     // value
};

// Iterator class would also need to be defined similarly without templates
class Map::Iterator {
  // Iterator implementation that works with Map::Entry
  // ...
};
```

### Hash Tables

One of the most efficient ways to implement a map is to use a hash table.
- Usual time complexity for operations $O(1)$ with worst case $O(n)$

#### Bucket Arrays
A **bucket array** for a hash table is an array $A$ of size $N$ ,where each cell of $A$ is thought of as a "bucket" (a collection of entries(key, value pairs)).
An entry $e$ with key $k$ is simply inserted into the bucket $A[k]$
![[image-7.png]]
Drawbacks:
- There is a lot of wasted space within the array
- The keys are required to be integers in the range $[0, N-1]$
Due to this we will use the bucket array in conjunction with a "good" mapping from keys to the integers in the range $[0, N-1]$.
#### Hash Functions
The **hash function** maps each key $k$ in our map to an integer in the range $[0, N-1]$, where $N$ is the capacity of the bucket array for this table.
- We can use the hash function value $h(k)$ as an index into our bucket array $A$, instead of just key $k$. This index is called the *hash value*. 
- So, we store entry $(k, v)$ in the bucket $A[h(k)]$.
- If there are two or more keys with the same hash value, then two different entries will be mapped to the same bucket in $A$. This is a *collision*, a collision results in a time complexity that is typically $O(n)$ rather than our desired $O(1)$. 
- The best strategy to combat this is to create a "good" hash function. Where a "good" hash function minimizes collisions as much as possible whilst being fast and easy to compute.



We view the evaluation of the hash function $h(k)$ as consisting of two actions:
1) Mapping the key $k$ to the hash code
2) Mapping the hash code to an integer within the range of indices $[0,N-1]$ of a bucket array, called the *compression* function

![[0903.png]]

#### Hash Codes
The integer assigned to a key $k$ is called the **hash code** for $k$. 

Hash codes vs. Hash values:
- Often used interchangeably with *hash values*. 
- But there is a difference if you were to speak technically:
	- *Hash codes:* Integer assigned to a key. 
	- *Hash values:* Index of array $A$ (index of the hash table).