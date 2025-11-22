#DataStructures 

- selection sort
My way (might not work):
```C++
void sort(int A[], int size) {
	if (size == 0) return;
	int largest = 0;
	int largestIndex = 0;
	for (int i = 0; i < size; i++) {
		if (A[i] >= largest)
			largestIndex = i;
		if (i == size-1) {
			int temp = A[size];
			A[largestIndex] = A[size];
			A[largestIndex] = temp;
		}
	}
	sort(A, size-1);
}
```

In class:
```C++
void selection_sort(int A[], int n) {
	// visualization
	// sorted subarray: (i, n-1]
	// unsorted subarray: [0, i)
	// initial state: [0, n-1] , (n-1, n-1]
	for (int i = n-1; i > 0; i--) {
		int pos = 0;
		for (int j = 1; j <= i; j++)
			if (A[j] > A[pos])
				pos = j;
		swap(A[pos], A[i]);
	}
}
```
Time Complexity Analysis:
$$\sum_{i=1}^{n-1}\sum_{j=1}^{i}1 = \sum_{i=1}^{n-1}i = \frac{n-1(n-1+1)}{2}= \frac{n(n-1)}{2}=\frac{n^2-n}{2}$$
- Since $n^2$ is dominant $T(n) = O(n^2)$

### Bubble Sort
Waves pushing largest to shore…

iterative:
```C++
void bubble_sort(int A[], int n) {
	// unsorted subarray: [0, i]
	// sorted subarray: (i, n-1]
	for (int i = n-1; i > 0; i--) {
		for (int j = 0; j+1 <= i; j++)
			if (A[j] > A[j+1])
				swap(A[j], A[j+1]);
	}
}
```
Time Complexity Analysis:
$$\sum_{i=1}^{n-1}\sum_{j=1}^{i}1 = \sum_{i=1}^{n-1}i = \frac{n-1(n-1+1)}{2}= \frac{n(n-1)}{2}=\frac{n^2-n}{2}$$
- Since $n^2$ is dominant $T(n) = O(n^2)$
recursive:
```C++
void bubble_sort(int A[], int n) {
	if (n <= 1) return;
	for (int i = 0; i+1 < n; i++)
		if (A[i] > A[i+1])
			swap(A[n], A[n+1]);
	bubble_sort(A, n-1);
}
```
