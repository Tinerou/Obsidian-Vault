#DataStructures 
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
### **Static Array:** list.cpp
```C++
#include<iostream>
#include"list.h"

List::List() : count(0) {}

bool List::empty() {
  return !count;
}

bool List::insert(ElementType x, int pos) {
  if(pos < 0 || pos > count || count >= SIZE) return false;
  for(int i = count; i > pos; i--) {
    arr[i] = arr[i-1];
  }
  arr[pos] = x;
  count++;
  return true;
}

bool List::erase(int pos) {
  if(pos < 0 || pos >= count) return false;
  for(int i = pos+1; i<count; i++) {
    arr[i-1] = arr[i];
  }
  count--;
  return true;
}

void List::display(std::ostream& out) const {
  for (int i = 0; i < count; i++) {
    out << arr[i] << std::endl;
  }
}

std::ostream& operator<<(std::ostream& out, const List& list) {
  list.display(out);
  return out;
}
```
### **Dynamic Array:** list.h
```C++
#ifndef LIST_H
#define LIST_H
#include<iostream>

typedef int ElementType;
class List {
private:
  ElementType* arr;
  int count, size;
public:
  List(int c = 10);
  ~List();
  List(const List& other);
  const List& operator=(const List& other);
  bool empty() const;
  bool insert(ElementType x, int pos);
  bool erase(int pos);
  void display(std::ostream& out) const;
};
std::ostream& operator<<(std::ostream& out, const List& list);

#endif
```
### **Dynamic Array:** list.cpp
```C++
#include"list.h"
#include<iostream>

List::List(int c) : size(c) {
  count = 0;
  arr = new ElementType[size];
}

List::~List() {
  delete[] arr;
}

List::List(const List& other) {
  count = 0;
  size = other.size;
  arr = new ElementType[size];
  for(int i = 0; i < other.count; i++) {
    insert(other.arr[i], i);
  }
}

const List& List::operator=(const List& other) {
  if(this == &other) return *this;
  delete[] arr;
  count = 0;
  size = other.size;
  arr = new ElementType[size];
  for (int i = 0; i < other.count; i++) {
    insert(other.arr[i], i);
  }
  return *this;
}

bool List::empty() const {
  return !count;
}

bool List::insert(ElementType x, int pos) {
  if(pos < 0 || pos > count || count >= size) return false;
  for(int i = count; i > pos; i--) {
    arr[i] = arr[i-1];
  }
  arr[pos] = x;
  count++;
  return true;
}

bool List::erase(int pos) {
  if(pos < 0 || pos >= count) return false;
  for(int i = pos; i < count-1; i++) {
    arr[i] = arr[i+1];
  }
  count--;
  return true;
}

void List::display(std::ostream& out) const {
  for(int i = 0; i < count; i++) {
    out << arr[i] << std::endl;
  }
}

std::ostream& operator<<(std::ostream& out, const List& list) {
  list.display(out);
  return out;
}
```
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

## Linked List

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
```C++
class SinglyLinkedList {
private:
  struct Node {
    int data;
    Node* next;
    Node(int data, Node* next=nullptr) {
      this->data = data;
      this->next = next;
    }
  };
  int n; // size counter
  Node* head;
public:
  SinglyLinkedList() {
    n = 0;
    head = nullptr;
  }
  SinglyLinkedList(const int& data) {
    n = 0;
    head = nullptr;
    insert(data);
  }
  SinglyLinkedList(const SinglyLinkedList& other) {
    n = 0;
    Node* temp = other.head;
    for(int i = 0; i < other.size(); i++) {
      insert(temp->data);
      temp = temp->next;
    }
  }
  ~SinglyLinkedList() {
    while(!empty()) {
      remove();
    }
  }

  SinglyLinkedList& operator=(const SinglyLinkedList& other) {
    if(this == &other) return *this;
    while(!empty()) {
      remove();
    }
    Node* temp = other.head;
    for(int i = 0; i < other.size(); i++) {
      insert(temp->data);
      temp = temp->next;
    }
    return *this;
  }
  void insert(const int& data) {
    head = new Node(data, head);
    n++;
  }
  void remove() {
    if(!empty()) {
      Node* temp = head;
      head = head->next;
      delete temp;
      n--;
    }
  }
  bool empty() const {
    return !n;
  }
  int size() const {
    return n;
  }
  void swapPair(Node* head) {
    if(head == nullptr || head->next == nullptr) return;
    int temp = head->next->data;
    head->next->data = head->data;
    head->data = temp;
    swapPair(head->next->next);
  }
  
};

```

### Doubly-linked list

![[Pasted image 20251006095924.png]]
- Often sacrifice Head and Tail to make code more simplified
	- Used more in real-world situations
 