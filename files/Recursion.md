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

**Recursion**

```C++
int binarySearch(int A[], int low, int high, int target) {
  // base case (fail)
  if(low > high) return -1;
  // setup
  int mid = low+((high-low)/2);
  // recursive function
  if(target < A[mid]) {
    return binaryS(A, low, mid-1, target);
  }
  if(target > A[mid]) {
    return binaryS(A, mid+1, high, target);
  }
  // base case (success)
  return mid;
}
```

**Permutation**
```C++

void permutation(int arr[], bool used[], int size, int index, int permu[]) {

  // base case
  if (index == size) {
    for (int k = 0; k < size; k++) {
      std::cout << permu[k] << " ";
    }
    std::cout << std::endl;
    return;
  }
  
  // recursive step
  // find an unused integer and put it into our current permutation 
  for(int k = 0; k < size; k++) {
    if (used[k]) continue;
    used[k] = true;
    permu[index] = arr[k];
    permutation(arr, size, used, permu, index+1);
    used[k] = false;
  }
}
```

**Subset**
```C++
void subset(int A[], int n, int i, int j, int S[]) {

  // base case
  if (i == n) {
    for (int k = 0; k < j; k++) {
      std::cout << S[k] << " ";
    }
    std::cout << endl;
    return;
  }

  // Recursive step: examining A[]
  // int j is the size of A[]
  subset(A, n, i+1, j, S);
  S[j] = A[i];
  subset(A, n, i+1, j+1, S);
}
```