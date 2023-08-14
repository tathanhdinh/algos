#### Soient $c,s \in \mathfrak{S}(E)$ où $c = (a_1 \ a_2 \ \dots \ a_n)$ un $n$-cycle, alors

$$
\begin{align}
\left(a_1 \ a_2 \ \dots \ a_n\right) = (a_1 \ a_2) \circ (a_2 \ a_3) \circ \dots \circ (a_{n-1} \ a_n) \\
s \circ \left(a_1 \ a_2 \ \dots \ a_n\right) \circ s^{-1} = \left(s(a_1) \ s(a_2) \ \dots \ s(a_n)\right)
\end{align}
$$

Démonstration.

Considérons le second membre de l'égalité $(1)$:

$$
\begin{align*}
&a_n \mapsto a_{n-1} \mapsto a_{n-2} \mapsto \dots \mapsto a_2 \mapsto a_1 \\
&a_{i} \mapsto a_{i+1} \ \forall i \neq n
\end{align*}
$$

L'égalité $(2)$ se réécrit:

$$
s \circ \left(a_1 \ a_2 \ \dots \ a_n\right) =  \left(s(a_1) \ s(a_2) \ \dots \ s(a_n)\right) \circ s
$$

Pour le premier membre $a_i \mapsto a_{i+1} \mapsto s(a_{i+1})$, pour le second membre $a_{i} \mapsto s(a_{i}) \mapsto s(a_{i+1})$.

#### Soient $n \geq 2$ un entier, et

$$
\begin{align*}
S & \coloneqq \{ (1 \ 2), (2 \ 3), \dots, (n-1 \ n)  \} \\
T & \coloneqq \{ (1 \ 2), (1 \ 3), \dots, (1 \ n) \} \\
U & \coloneqq \{ (1 \ 2), (1 \ 2 \ \dots \ n) \}
\end{align*}
$$

alors $\langle S \rangle = \langle T \rangle = \langle U \rangle = \mathfrak{S}(E)$.

Démonstration.

Considérons $(1 \ k) \circ (1 \ k+1)$:

$$
\begin{align*}
& (1 \ k+1) &  & (1 \ k) \\
1 &\mapsto& k+1 &\mapsto &k+1 \\
k &\mapsto   &k & \mapsto & 1 \\
k+1 & \mapsto & 1 &  \mapsto &  k
\end{align*}
$$

alors $(1 \ k+1) \circ (1 \ k) \circ (1 \ k+1) = (k \ k+1)$:

$$
\begin{align*}
& (1 \ k+1) &  & (1 \ k) & & (1 \ k+1) \\
1 &\mapsto& k+1 &\mapsto  &k+1 & \mapsto & 1 \\
k &\mapsto   &k & \mapsto  &1 & \mapsto & k+1\\
k+1 & \mapsto & 1 &  \mapsto &  k & \mapsto & k
\end{align*}
$$

d'où $\langle S \rangle \subseteq \langle T \rangle$.

Puisque $(1 \ 2 \dots \ n) \circ (k-1 \ k) \circ {(1 \ 2 \dots \ n)}^{-1} = (k \ k+1)$ for all $k \in \llbracket 2, n \rrbracket$, de plus $(1 \ 2) \in U$, alors $\langle S \rangle \subseteq \langle T \rangle$.



<!-- $$
(1 \ k) \circ (1 \ k+1) = \bigl(\begin{smallmatrix} 1 & \dots & k & \dots \\ k & \dots & 1 & \dots \end{smallmatrix} \bigr) \circ \bigl(\begin{smallmatrix} 1 & \dots & k+1 & \dots \\ k+1 & \dots & 1 & \dots \end{smallmatrix} \bigr) = \bigl(\begin{smallmatrix} 1 & \dots & k & k+1 & \dots \\ k+1 & \dots & 1 & k &\dots \end{smallmatrix}\bigr)
$$ -->