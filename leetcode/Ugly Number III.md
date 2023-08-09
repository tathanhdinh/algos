#### Problem: [Ugly number III](https://leetcode.com/problems/ugly-number-iii/)

> An ugly number is a positive integer that is divisible by a, b, or c.
>
> Given four integers n, a, b, and c, return the nth ugly number.

#### Idea
Using formula for the priciple of inclusion-exclusion, for any $m \in \mathbb{N}^{*}$, the number of multipliers which are less than or equal $m$ of either $a$, $b$ or $c$ is:

$$
n = \left\lfloor \frac{m}{a} \right\rfloor + \left\lfloor \frac{m}{b} \right\rfloor + \left\lfloor \frac{m}{c} \right\rfloor - \left\lfloor \frac{m}{\text{lcd}(a,b)} \right\rfloor - \left\lfloor \frac{m}{\text{lcd}(a,c)} \right\rfloor - \left\lfloor \frac{m}{\text{lcd}(b,c)} \right\rfloor + \left\lfloor \frac{m}{\text{lcd}(a,b,c)} \right\rfloor
$$

So knowing $n$, we can estimate the upper and the lower bound for $m$, from that the exact value of $m$ (*i.e. the ugly number*) can be determined.

#### Code

```rust
fn nth_ugly_number(n: i32, a: i32, b: i32, c: i32) -> i32 {
    fn pgcd(x: u128, y: u128) -> u128 {
        let (mut x, mut y) = (x, y);
        loop {
            let r = x % y;
            if r == 0 {
                break y;
            }
            x = y;
            y = r;
        }
    }

    fn ppcm(x: u128, y: u128) -> u128 {
        x * (y / pgcd(x, y))
    }

    let (n, a, b, c) = (n as u128, a as u128, b as u128, c as u128);
    let (ppcm_ab, ppcm_ac, ppcm_bc) = (ppcm(a, b), ppcm(a, c), ppcm(b, c));
    let ppcm_abc = ppcm(a, ppcm(b, c));

    let count =
        |n: u128| n / a + n / b + n / c + n / ppcm_abc - n / ppcm_ab - n / ppcm_ac - n / ppcm_bc;

    let q = ppcm_abc / a + ppcm_abc / b + ppcm_abc / c + 1
        - ppcm_abc / ppcm_ab
        - ppcm_abc / ppcm_ac
        - ppcm_abc / ppcm_bc;

    let upper_bound = (n + 3u128) * ppcm_abc / q + 1;
    let lower_bound = if n <= 3u128 {
        0u128
    } else {
        (n - 3u128) * ppcm_abc / q
    };

    for k in lower_bound..=upper_bound {
        if count(k) == n {
            return k as i32;
        }
    }

    0
}
```

#### Complexity:
The upper/lower bounds can be calculated directly from $n$ (and $a,b,c$), and their difference does not depend on $n$,so the complexity is $\mathcal{O}(1)$.