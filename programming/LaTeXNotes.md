
#### Plain text 
`\text{Hi, here is some math}`
#### Relation operators
https://oeis.org/wiki/List_of_LaTeX_mathematical_symbols

| Symbol  | LaTeX   | Comment                  |
| ------- | ------- | ------------------------ |
| $\leq$  | `\leq`  | less than or equal to    |
| $\geq$  | `\geq`  | greater than or equal to |
| $\neq$  | `\neq`  | not equal to             |
| $\ngeq$ | `\ngeq` | you can combine these!   |

#### Complement

| Package   | Command           | Output          |
| --------- | ----------------- | --------------- |
| `amssymb` | `$A^\complement$` | $A^\complement$ |
| none      | `$A^\prime$`      | $A^\prime$      |
| none      | `$\overline{A}$`  | $\overline{A}$  |
More at: https://www.codespeedy.com/set-complement-symbol-in-latex/

#### Sum

```LaTeX
$$\begin{equation}
\sum^{n-1}_{j=i}{j-i+1}
\end{equation}$$
```
Displays as: $$\begin{equation}
\sum^{n-1}_{j=i}{j-i+1}
\end{equation}$$
Inline
``` LaTeX
$\sum^{n-1}_{j=i}{j-i+1}$
```
Displays as : $\sum^{n-1}_{j=i}{j-i+1}$

Note: the sub and superscript order for the sum are interchangeable