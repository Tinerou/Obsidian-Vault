### **Static Array:** list.h
``` C++
#ifndef _LIST_H  
#define _LIST_H  
#include <ostream>  
const int SIZE = 1000;  
typedef int ElementType;  
class List {  
private:  
	ElementType arr[SIZE];  
	int count;  
public:  
	List();  
	~List();  
	bool empty();  
	bool insert(ElementType x, int pos);  
	// - Input validation (check if pos is valid)
	// - Make rooom for new elements (shift elements if needed)
	// - sort (array[pos] = x)
	// - update count
	bool erase(int pos);  
	void display(std::ostream& out) const;  
};  
	std::ostream& operator<<(std::ostream& out, const List& list);  
#endif
```
**ADT: List**

Static Array:
- Pros: 
	- simple
- const: 
	- one size fits all

Dynamic Array:
- Pros: 
	- More flexibility
- Cons: 
	- Complexity: Copy constructor, assignment operator, destructor
		- assignment operator: to avoid shallow copy
		- destructor: to avoid memory leak
- 
### Stages of design
**Stage 1**: Design
- Data members
- Operations (member functions)
**Stage 2**: Implementation
- Data structures (containers)
- Algorithms

### Linked List

Contents: 
- Data - stores an element of the list
- Pointer to next - Stores link/pointer to a node carrying next element
	- When no next element, NULL value

Basic Operation:
- Traversal:
	- Initialize a variable `ptr` to point to first node
	- Process data where `ptr` points
- Insertion: 
	- Linear traversal
		- Must traverse through each element
	- Note: Linked list shine when you need to insert or delete the beginning or end node
- Deletion:
	- Linear traversal
	- Update the head pointer

Things to check:
 - Before operating on a pointer make sure pointer is NULL.

Pros: 
- Access any item as long as external link to first item maintained
- Insert/delete without shifting
- Can expand/contract as necessary
Cons:
- Overhead of links
- Somewhat complex: destructor, copy constructor, assignment operator
- No direct access to each element
- Access of the *n*th item is now less efficient

### Doubly-linked list

![[Pasted image 20251006095924.png]]
- Often sacrifice Head and Tail to make code more simplified
	- Used more in real-world situations
 