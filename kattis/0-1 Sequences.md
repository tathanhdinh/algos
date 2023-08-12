#### Problem [0-1 Sequences](https://open.kattis.com/problems/sequences)

>You are given a sequence, in the form of a string with characters `0`, `1`, and `?` only. Suppose there are $k$ `?`(s). Then there are $2^k$ ways to replace each `?` by a `0` or a `1`, giving different `0-1` sequences (`0-1` sequences are sequences with only zeroes and ones).
>
>For each `0-1` sequence, define its number of inversions as the minimum number of adjacent swaps required to sort the sequence in non-decreasing order. In this problem, the sequence is sorted in non-decreasing order precisely when all the zeroes occur before all the ones. For example, the sequence $11010$ has inversions. We can sort it by the following moves: $11010 \to  11001 \to 10101 \to 01101 \to 01011 \to 00111$.
>
>Find the sum of the number of inversions of the $2^k$ sequences, modulo $1.000.000.007$ ($10^9+7$).

#### Solution
We first consider the number of inversions of a sequence.