#### Bit-shifting [method](https://en.wikipedia.org/wiki/Methods_of_computing_square_roots#Binary_numeral_system_(base_2))

Let $s = a_n + a_{n-1} + \dots + a_{0}$ where

$$
a_i =
\begin{cases}
    2^i & \text{if the } i\text{-th bit is } 1 \\
    0 & \text{otherwise}
\end{cases}
$$

be the binary representation of the square root of $x$, and $s_{i}$  be the partial sum

$$
s_i = a_n + \dots + a_{i}
$$

Let's consider how to calculate the next $s_{i-1}$, or more precisely to calculate $ss_{i-1} = 2^{i-1}  s_{i-1}$. It depends on the comparison:

$$
\begin{align*}
(s_i + 2^{i-1})^2 \leq x & \iff  {s_i}^{2} + s_i 2^{i} + 2^{2i-2} \leq x \iff s_i 2^{i} + 2^{2i-2} \leq x - {s_{i}}^{2} \\
& \iff ss_{i} + 2^{2i-2} \leq x - {s_i}^{2}
\end{align*}
$$

So we compare $ss_i + 2^{2i-2}$ against $x - {s_{i}}^{2}$:
 - if it is smaller or equal then

$$
ss_{i-1} = 2^{i-1}s_{i-1} = 2^{i-1}(s_{i} + 2^{i-1}) = \frac{ss_{i}}{2} + 2^{2i-2}
$$

 - otherwise

$$
ss_{i-1} = 2^{i-1}s_{i-1} = 2^{i-1}s_{i} = \frac{ss_{i}}{2}
$$

Correspondingly, $d_{i-1} = x - {s_{i-1}}^2$ can be calculated by
 - either

$$
d_{i-1} = x - (s_i+2^{i-1})^2 = x - {s_i}^{2} - 2^{i}s_{i} - 2^{2i-2} = d_{i} - ss_i - 2^{2i-2}
$$

 - or

$$
d_{i-1} = x - {s_{i}}^2 = x - {s_{i-1}}^2 = d_{i}
$$

We use this recurrence relation to calculate

$$
ss_0 = 2^{0} s_{0} = s
$$

Note that $s_n = 2^n$ where $n$ is the largest number being satisfy $2^{2n} \leq x$, hence

$$
\begin{align*}
ss_n &= 2^n s_n = 2^{2n} \\
d_n &= x - {s_n}^2 = x - 2^{2n}
\end{align*}
$$

#### Implementation

Consider this leetcode [problem](https://leetcode.com/problems/sqrtx):

> Given a non-negative integer $x$, return the square root of $x$ rounded down to the nearest integer. The returned integer should be non-negative as well.
>
> You must not use any built-in exponent function or operator.

```Rust
fn my_sqrt(x: i32) -> i32 {
    let mut b = 1 << 30; // 2^{2i}
    while b > x {
        b = b >> 2;
    }

    let (mut ss, mut d) = (b, x - b);
    while b > 1 {
        b = b >> 2;

        if ss + b <= d {
            d = d - ss - b;
            ss = (ss >> 1) + b;
        } else {
            ss = ss >> 1;
        }
    }

    ss
}
```