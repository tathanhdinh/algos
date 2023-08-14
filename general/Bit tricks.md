#### Isolate the lowest bit of $x$ that is $1$:

$$
y = x \land \lnot{(x-1)}
$$

Example:

$$
\begin{align*}
x &= 010100 \\
x-1 &= 010011 \\
\lnot{x-1} &= 101100 \\
y = x \land \lnot{(x-1)} &= 000100
\end{align*}
$$

Explanation:

Suppose that the $i$-th bit is the lowest bit of $x$ that is $1$, that means all lower bits are $0$, and
 - $x-1$ has its $i$-th bit is $0$, all lower bits are $0$, all higher bits are unchanged,
 - $\lnot{(x-1)}$ has its $i$-th bit is $1$, all lower bits are $1$, all higher bits are negated,
 - $x \land \lnot{(x-1)}$ has its $i$-th bit is $1$, all other bits are $0$.
