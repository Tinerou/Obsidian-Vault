
#### Basic Template
``` LaTeX
\begin{align}
place body in here
\end{align}
```
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
#### Dynamic Parenthesis
- Use `\left` before left parenthesis
- Use `\right` before right parenthesis
- `\left(     some maths here     \right)`
Example:
`\left( \sum_{34}^{n*93} \frac{n}{2} \right)`
$$\left( \sum_{34}^{n*93} \frac{n}{2}\right)$$
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

### Latex Suite Obsidian
https://github.com/artisticat1/obsidian-latex-suite?tab=readme-ov-file#cheatsheet
- Worth learning if you use LaTeX often in Obsidian
