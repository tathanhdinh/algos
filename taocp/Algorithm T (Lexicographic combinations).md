#### Description

The algorithm T is presented in the section 7.2.1.3 (volume 4A), it generates all $t$ combinations of $n$ numbers $\{ 0,1,\dots,n-1 \}$.

> T1. [Initialize.] Set $c_j \leftarrow j$ for $0 \leq j \leq t-1$; then set $c_t \leftarrow n, c_{t+1} \leftarrow 0$, and $j \leftarrow t$
>
> T2. [Visit.] (At this point $j$ is the smallest index such that $c_{j+1} > j+1$). Visit the combination $c_{t-1}\dots c_2 c_1$. Then, if $j\geq0$, set $x\leftarrow j+1$ and go to step T6.
>
> T3. [Easy case?] If $c_0 + 1 < c_1$, set $c_0 \leftarrow {c_1+1}$ and return to T2. Otherwise set $j \leftarrow 1$.
>
> T4. [Find $j$.] Set $c_{j-1} \leftarrow {j-1}$ and $x \leftarrow {c_j+1}$. If $x=c_{j+1}$, set $j \leftarrow {j+1}$ and repeat step T4.
>
> T5. [Done?] Terminate the alogrithm if $j \geq t$.
>
> T6. [Increase $c_j$.] Set $c_j \leftarrow x, j \leftarrow {j-1}$, and return to T2. $\quad \blacksquare$

#### Explanation

Consider an example where $n=6$ and $t=3$, then $\binom{6}{3} = 20$ combinations generated in order are:

$$
\begin{align*}
210,310,320,321, 410, 420, 421, 430, 431, 432,\\
510,520,521,530,531,532,540,541,542,543
\end{align*}
$$

Concretely:
- initialize $c_2 c_1 c_0 = 210$ (T1), note that $c_3= 6, c_4 = 0$
- only $c_2$ can be increased, increase $c_2=3$, receive $310$,
- continue (T2, T6):
  - set $c_1$ to $1+1$ receive $320$,
  - then set $c_0$ to $0+1$, receive $321$,
- go backward (T3, T4) to find the smallest index which can be increased:
  - 0 is not possible (since $c_0 + 1 = 1 + 1 = c_1$), reset $c_0$ to $0$,
  -  1 is not possible (since $c_1 + 1 = 2+1 = c_2$), reset $c_1$ to $1$,
  - 2 is possible (since $c_2 + 1 = 4 < c_3 = 6$), set $c_2 = 4$, receive $410$.
- if the smallest index is $3$ (T5) then stop.

The main idea of this algorithm is to compute the next number: when $c_j$ is increased, then $c_{j-1}, c_{j-2}, \dots c_0$ are reset to $j-1, j-2, \dots 0$, we receive the combination $$c_j(j-1)(j-2) \dots 10$$
The next numbers are:

$$
\begin{align*}
&c_jj(j-2) \dots 10, \\
&c_jj(j-1)\dots 10, \\
&\dots \quad \dots \quad \dots \\
&c_jj(j-1) \dots 20\\
&c_jj(j-1) \dots 21
\end{align*}
$$

#### Implementation

Consider this leetcode [problem](https://leetcode.com/problems/combinations):

> Given two integers $n$ and $k$, return all possible combinations of $k$ numbers chosen from the range $[1, n]$.

```rust
fn combine_t(n: i32, k: i32) -> Vec<Vec<i32>> {
    let (n, k) = (n as usize, k as usize);
    let mut out = vec![];

    // T1: initialize
    let mut c: Vec<_> = (1..=(k as i32)).collect();

    c.push(n as i32 + 1);
    c.push(0);
    let mut j = k - 1;

    loop {
        // T2: j is the first index for which c[j+1] > (j+1) + 1
        out.push(c[0..k].to_vec());

        if j > 0 {
            c[j] = (j as i32 + 1) + 1;
            j -= 1;
            continue;
        }

        // T3
        if c[0] + 1 < c[1] {
            c[0] += 1;
            continue;
        }

        // T4
        while c[j] + 1 == c[j + 1] {
            c[j] = j as i32 + 1;
            j += 1;
        }

        // T5
        if j >= k {
            break;
        }

        // T6
        c[j] += 1;
        j -= 1;
    }

    out
}
```