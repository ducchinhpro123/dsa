---
layout: post
title: "Quick Sort"
date: 2025-06-04
categories: jekyll update
---


# Overview

The idea of quicksort is simple, you have an array of n elements, you take the `p` element from the array of `n` elements, remaining n - 1 elements.
You denote that the `p` element in here is a `pivot`. For each element in the array n - 1 elements, the element that smaller than `pivot` will
go to the left of it, the element that greater than `pivot` will go to the right of it.

For example:

```
array: 3 7 8 5 2 1 9 5 4
                       p

less than `p`: 3 2 1
greater than `p`: 7 8 5 9 5

then: 3 2 1 "4" 7 8 5 9 5
             p
```


It's just compare, swap and recursion to divide then again until it meets a condition. Just that, what can be more difficult? What are you thinking about?

Demonstration taken from the book: The Algorithm Design Manual by Steven S. Skiena - Third Edition, Page 131.

![demo](/dsa/assets/images/quicksort.png)

Take the pointer `p`, divide the array into two parts: one part from `l` to `p - 1` and the other range from `p+1` to `h`.

```c
void quicksort(char** unsorted, int l, int h)
{
    if (l < h) {
        int p = partition(unsorted, l, h);
        quicksort(unsorted, l, p-1);
        quicksort(unsorted, p+1, h);
    }
}
```

In `partition` function, what can we do? we compare the goddamn string to see if it is less than the `pivot`, oh is it? then swap.


```c
int partition(char** unsorted, int l, int h)
{
    char *p_char = unsorted[h];

    printf("pivot: %s\n", p_char);
    int first_high = l;

    for (int i = l; i < h; i++) {
        if (compare_string(unsorted[i], p_char) < 0) {
            swap(&unsorted[i], &unsorted[first_high]);
            first_high++;
        }
    }
    swap(&unsorted[h], &unsorted[first_high]);
    return first_high;
}
```


the `first_high` is the first element in the array from range `l` to `h`.

