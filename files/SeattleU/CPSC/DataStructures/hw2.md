#DataStructures 

### Goal: Create a dequeue using a doubly-linked list 

![[HW2.pdf]]


**Deque.h** 
```C++
#ifndef DEQUE_H
#define DEQUE_H

class Deque {
private:
  int n;
  struct Node {
    int data;
    Node* prev;
    Node* next;
    // by default prev=Null, next=NULL
    Node(int data, Node* prev=NULL, Node* next=NULL) {
      this->data = data;
      this->prev = prev;
      this->next = next;
    }
  };
  Node* head;
  Node* tail;
public:
  Deque(); // constructor
  Deque(const Deque& other); // copy constructor
  ~Deque(); // destructor
  Deque& operator=(const Deque& other); // Assignment operator
  bool empty() const; // check if empty
  unsigned int size() const; // return size
  int front() const; // get front data
  int back() const; // get back data
  void push_front(const int& data); 
  void push_back(const int& data);
  void pop_front(); // remove front data
  void pop_back(); // remove back data
};

#endif
```

**Deque.cpp**
```C++
#include<iostream>
#include"deque.h"

Deque::Deque() {
  n = 0;
  head = new Node(-1);
  tail = new Node(-1);
  head->next = tail;
  tail->prev = head;
}

// Can allocate to previously uninitiallized data
Deque::Deque(const Deque& other) {
  // Initialize new Deque to be copied
  n = 0;
  head = new Node(-1);
  tail = new Node(-1);
  head->next = tail;
  tail->prev = head;

// Copy data
  Node* temp = other.head->next;
  while(temp != other.tail) {
    push_back(temp->data);
    temp = temp->next;
  }
}

Deque::~Deque() {
  while(!empty()) {
    pop_front();
  }
  delete head;
  delete tail;
}

Deque& Deque::operator=(const Deque& other) {
// Check if data is attempting to be assigned to itself
  if (this == &other) return *this;
// delete old deque (keep head and tail)
  while(!empty()) {
    pop_front();
  }

// Copy data from "other" to new nodes 
  Node* temp = other.head->next;
  while(temp != other.tail) {
    push_back(temp->data);
    temp = temp->next;
  }
  return *this;
} 

bool Deque::empty() const {
  return !n;
}

unsigned int Deque::size() const {
  return n;
}

int Deque::front() const {
  return head->next->data;
}

int Deque::back() const {
  return tail->prev->data;
}

void Deque::push_front(const int& data) {
  // Create new node
  Node* newNode = new Node(data, head, head->next);
  // Everything around the new node must show it
  head->next->prev = newNode;
  head->next = newNode;
  n++;
}

void Deque::push_back(const int& data) {
  Node* newNode = new Node(data, tail->prev, tail);
  tail->prev->next = newNode;
  tail->prev = newNode;
  n++;
}

void Deque::pop_front() {
  if(!empty()) {
    Node* temp = head->next;
    head->next = temp->next;
    temp->next->prev = head;
    delete temp;
    n--;
  } 
}

void Deque::pop_back() {
  if(!empty()) {
    Node* temp = tail->prev;
    tail->prev = temp->prev;
    tail->prev->next = tail;
    delete temp;
    n--;
  }
}
```

**client.cpp**
```C++
//client.cpp

#include <deque>
#include <iostream>
#include <cassert>
#include "deque.h"

using namespace std;

int main() {
  // test default constructor
  Deque x;
  deque<int> x_shadow;
  // test empty() and size()
  assert(x.empty() == x_shadow.empty() && x.size() == x_shadow.size());

  //test push_back(), push_front(), front(), back()
  for (int i = 0; i < 100000; i++) {
    int val = rand() % 1000000007;
    if (rand() % 2) {
      x.push_back(val);
      x_shadow.push_back(val);
    } else {
      x.push_front(val);
      x_shadow.push_front(val);
    }
    assert(x.front() == x_shadow.front() && x.back() == x_shadow.back());
  }

  // test copy constructor
  Deque y = x, z;

  // test assingment operator
  z = y;

  // test pop_front(), pop_back()
  while (!x_shadow.empty()) {
    if (rand() % 2) {
      assert(y.front() == z.front() && y.front() == x_shadow.front());
      y.pop_front();
      z.pop_front();
      x_shadow.pop_front();
    } else {
      assert(y.back() == z.back() && y.back() == x_shadow.back());
      y.pop_back();
      z.pop_back();
      x_shadow.pop_back();
    }
  }
  assert(y.empty() && z.empty());

  assert(!x.empty());

  //destructor is tested, if nothing occure which means the destrucor behaves property
  return 0;
}
```

