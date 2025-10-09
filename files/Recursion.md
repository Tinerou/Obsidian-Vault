Note: In the industry we avoid recursion to avoid unwanted bugs
**What is recursion?:**
1) Repeat same task (smaller) - With same function call
2) "Stop sign" / base case / anchor case
#### Different view on recursion
**Recursive Definition:**
- Example: n! = n(n-1)!
- non-math examples are common too
**Recursive Procedure:
- Base (or anchor) case
- Recursive case:
	- Reduction step (can be the same as base case)
	- Recursive call
**Recursive Data Structure:**
A data structure that contains a pointer to an instance of itself
```C++
class Node {
public:
	int data;
	Node* next;
};
```

#### Recursion in Algorithms
- Recursion is a technique that is useful
	- for defining relationships
	- for designing algorithms that implement the relationship

```C++
int factorial(int n) {
	if (n==0) return 1; // base case
	return n * factorial(n-1) // recursive step
}
```

``` C++
// Find max value 1
int find_max(int A[], int n, int i) {
  if (i == n-1) return A[i];
  return max(find_max(A, n, i+1), A[i]));
}
```

``` C++
// Find max value 2
class Node {
public:
	int data;
	Node* next;
}

int find_max(Node* head, int i) {
	if (node->next) == NULL return node->data;
	return max(find_max(node->next), i)
} 
```

```C++
// Find max value 2 class version
int find_max(Node* head) {
	if(!head) return INT_MIN; // If head is null
	return max(head->data, find_max(head->next));
}
```
