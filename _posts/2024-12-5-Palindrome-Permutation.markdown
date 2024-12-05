---
layout: post
title: Palindrome Permutation
date: 2024-12-5
categories: jekyll update
---

# Problem

Palindrome Permutation: Given a string, write a function to check if it is a permutation of 
a palindrome. A palindrome is a word or phrase that is the same forwards and backwards. A 
permutation is a rearrangement of letters. The palindrome does not need to be limited to just 
dictionary words. 

> EXAMPLE 

> Input: Tact Coa 

> Output: True (permutations: "taco cat'; "atco eta·; etc.) 

# Approach

One simple approach is using the hashmap built-in in Java. And you should not generate all the permutations 
of the string because it is very inefficient. You see in the output every digits must be the even number except 
there is only one odd number, don't count space if it is irrevalent. Let's see with original String: `Tact Coa`

``` Example: 
-1 // We don't count this one
a-2
c-2
t-2
o-1
```

# Implementation

```java
boolean isPermutationOfPalindrome(String str) {
    HashMap<Character, Integer> map = new HashMap<>();
    char[] arr = str.toCharArray();
    for (int i = 0; i < arr.length; i++) {
        map.put(arr[i], map.getOrDefault(arr[i], 0) + 1);
    }

    boolean foundOdd = false;
    for (char key : map.keySet()) {
        if (key != ' ' && map.get(key) % 2 == 1) {
            if (foundOdd) return false;
            foundOdd = true;
        }
    }

    return true;
}
```

