When you write an algorithm you need to know:
- time complexity? 
	- time efficiency: T(n) = # of basic operations(most expensive operations)
- memory complexity?

By Big O definition:
If $T(n) =3n+4$ which is, $<=3n+n$ (when n>=4)

In theory, there is no upper bound but if you exceed what is actually there it is non-informative.

$\theta \omega$ 

Big O proofs:

Prove: $T(n) = 100n+logn$
$T(n) <= 100n+n$
Because $n>=logn$
$=101*n$
$=c*f(n)$
So,
$c*f(n) >= T(n)$
Therefore, $O(n) >= T(n)$ 

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
