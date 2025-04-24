---
layout: post
title: "Sum of powers of 2"
date: 2025-04-24
categories: jekyll update
---

# Sum of powers of 2

## Description

Given a number n, you should find a set of numbers for which the sum equals n. This set must consist exclusively of values that are a power of 2 (eg: 2^0 => 1, 2^1 => 2, 2^2 => 4, ...).

The function powers takes a single parameter, the number n, and should return an array of unique numbers.

Criteria
The function will always receive a valid input: any positive integer between 1 and the max integer value for your language (eg: for JavaScript this would be 9007199254740991 otherwise known as Number.MAX\_SAFE\_INTEGER).

The function should return an array of numbers that are a power of 2 (2^x = y).

Each member of the returned array should be unique. (eg: the valid answer for powers(2) is [2], not [1, 1])

Members should be sorted in ascending order (small -> large). (eg: the valid answer for powers(6) is [2, 4], not [4, 2])


## Work through

In previous posts, I usually work through it first before I provide the solution, but I think it would be better to give the code first, and then
working through it.

```c
#include <stdio.h>
#include <stdlib.h>

unsigned long long* powers(size_t* outlen, unsigned long long n)
{
    size_t c = 0;
    unsigned long long t = n;

    while (t > 0) {
        if (t & 1)
            c++;
        t >>= 1;
    }

    *outlen = c;

    unsigned long long* result = malloc(c * sizeof(unsigned long long));
    size_t index = 0;
    for (int i = 0; i < 64; i++) {
        if (n & (1ULL << i)) {
            result[index++] = (1ULL << i);
        }
    }

    return result;
}
```

In this problem, I will need to lighten some ambiguouses. Given a number `n`, find the sum of powers of 2 that equal `n`. For example, if `n` is 13 then
the numbers in array are: 1, 4, 8. Since the sum of it is equal to `n`.

1 is 2^0, 4 is 2^2, 8 is 2^3.
Look at 2^0, 2^2, 2^3, we see that 0, 2, 3. Where is the 1? That's _suspicious_. Ah! 13 in binary form is *1101*.


The condition: `if (n & (1ULL << i))` checks if the bit at position i in n is set. When we find a set bit, we store the corresponding power of 2 (2ⁱ).
`result[index++] = (1ULL << i)`


