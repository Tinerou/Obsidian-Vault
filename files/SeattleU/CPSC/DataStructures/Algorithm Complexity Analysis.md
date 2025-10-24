#DataStructures 
When you write an algorithm you need to know:
- time complexity? 
	- time efficiency: T(n) = # of basic operations(most expensive operations)
- memory complexity?

By Big O definition:
If $T(n) =3n+4$ which is, $<=3n+n$ (when n>=4)

In theory, there is no upper bound but if you exceed what is actually there it is non-informative.

### Summation to find Big-O

Note: 
$$\begin{align}
\sum^n_{i=m}1 = n-m+1 \\
\sum_{i=0}^n{i}=\sum_{i=1}^n{i}=\frac{n(n+1)}{2}  \\
\sum_{i=0}^nn=n(n+1)
\end{align}$$
Now find the Big-O notation of:
```C++
for(int i = 0; i <= n-1; i++) {
	for(int j = i+1; j<= n-1; j++) {
		// Loop body
	}
}
```

$$\begin{align}

\sum_{i=0}^{n-1}\sum_{i+1}^{n-1}1=\sum_{i=0}^{n-1}(n-1+(-i+1)+1)=\sum_{i=0}^{n-1}(n-i+1)\\=\sum_{i=0}^{n-1}n-\sum_{i=0}^{n-1}i+\sum_{i=0}^{n-1}1=n^2-\frac{n-1(n-1+1)}{2}+n-1+1 \\
=n^2-\frac{n^2-n}{2}+n=\frac{2n^2}{2}-\frac{n^2-n}{2}-\frac{2n}{2}\\=\frac{n^2-n}{2} \text{ becuase } n^2 \text{ is the highest, big-O is:}\\O(n^2)

\end{align}$$


$\theta \omega$ 

Big O proofs:

Prove: $T(n) = 100n+logn$
$T(n) \leq 100n+n$
Because $n\geq logn$
$=101*n$
$=c*f(n)$
So,
$c*f(n) \geq T(n)$
Therefore, $O(n) \geq T(n)$ 

$T(n)=7n-2$
$T(n) <= 7n +n$
$=8*n$
$=c*n$
$= c*f(n)$
So, 
$c*f(n)>=T(n)$
Therefore, O(n) = T(n)

$T(n) = 3n^3 +20n^2+5$
$T(n) <= 3n^3 + 20n^2*n +5*n^3$
$=(3n^3+20n^3+5n^3)$
$28*n^3$
$=28*f(n^3)$
$=c*f(n^3)$
So,
$c*f(n^3) >= T(n)$
Therefore, $O(n^3) = T(n)$

$T(n)=3logn+5$
$T(n) <= 3logn+5logn$
$=8logn$
$=c*logn$
$= c*f(logn)$
So,
$c*f(logn)>=T(n)$
Therefore, $O(logn) = T(n)$

**Given an algorithm, we need to find $T(n)$**
1) Input size $n$
2) What is the basic operation?
3) $T(n)$ = Number of basic operations (worst case)
4) $T(n) = O(f(n))$

**Shortcut**
1) Use the input size $n$ rather than the input itself
2) Identify the basic operation and determine its execution count in the worst case
3) Drop items with lower degree and drop constant factors
4) Big-O estimate gives an approximate measure of the computing time of an algorithm for large inputs

n
input size: ;a.size() = $n$
Basic operation: thisSum += $a[k]$
Worst case: j(j-i+1)
$n*n*n=n^3$ 
$j\subset{i,n-1}$
$$\begin{equation}
\sum^{n-1}_{j=i}{j-i+1}
\end{equation}$$

Input size = size of vector a = $n$
Basic operation: thisSum+=$a[j]$ and/or key comparison maxSum=thisSum
Worst case: $i(n-i)$ = n(n-n) = $n^2$
$O(n^2)$

Input size = size of vector a  = $n$
Basic operation: key comparison
Worst case: (n-1)1
$O(n)$

$2/n, \sqrt{n}, n, \log n, n\log n, n^{1.5}, n^3/100, n^4 \log n, 2^n$
lowest->highest

Big-O for recursive Algorithms
1) ...
``` C++
double power(doublex, unsigned n) {
	// base case
	if (n==0) return 1.0; //T(0) = O(1)
	return x*pow(x,n-1)
}
```
base case: $T(0) = O(1)$
$x^n$->$x^{n-1}$
recursive function: $T(n) = T(n-1) + 1$
$T(n) = T(n-1) + 1$
$T(n-1) = T(n-2) +1$
$T(n-2) = T(n-3) +1$
...
$T(2) = T(1)+1$
$T(1) = T(0)+1$
We do this $n$ times so $O(n)$


T(n=0) = O(1)
T(n) = T(n/2)+1
T(n/2) = T(n/2)+1
T(n/2^2) = T(n/2^2)+1
...
T(2) = T(1)/2
T(1) = T(0)/2
$O(\log n)$

