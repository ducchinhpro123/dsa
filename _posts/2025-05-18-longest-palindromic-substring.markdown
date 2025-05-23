---
layout: post
title: "Longest Palindromic Substring"
date: 2025-05-23
categories: jekyll update
---

> If you are interested about this problem, please visit this [link](https://leetcode.com/problems/longest-palindromic-substring/) for more information about the problem description.


This post expresses a way of thinking by using dynamic programming technique.


## Understand the problem

You are given a string and you want to get the longest palindromic substring.

A string is palindromic if it reads the same forward and backward. Example: `racecar`, `bab`

```
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
```

## Work through problem

The string is, for example: `bananas`, we found a substring is a palindromic which is `ana` and another one `anana`

The problem is asking to return the longest substring that is palindromic so we will return `anana`

So how the problem will be solved?

Well, let's use dynamic programming technique.

> Dynamic programming is not so hard, i think the hardest part of it is how we construct the solution, how we find a formula for that.

- if there is only one character then it is a substring palindromic.
- if there are two characters, check if it is equal.
- if there are more than two characters, for example: `cbabc`, the first character `c` and the last character is `c`
Do they equal? Yes, but is the inside of it is palindromic too? `bab`? yes.

```

if len = 1:
    dp[i][j] <- true
if len = 2:
    dp[i][j] <- s[i] == s[j]
else:
    dp[i][j] <- s[i] == s[j] and dp[i+1][j-1]
```

`i+1` and `j-1` is s[i+1] to s[j - 1], which is inside of the string s[i] to s[j]

## The code

```c
    for (int len = 1; len <= n; len++) {
        for (int i = 0; i <= n - len; i++) {
            int j = i + len - 1;
            if (len == 1) {
                dp[i][j] = 1;
            } else if (len == 2) {
                dp[i][j] = s[i] == s[j];
            } else {
                dp[i][j] = (s[i] == s[j] && dp[i+1][j-1]);
            }

            if (dp[i][j] && len > max_len) {
                max_len = len;
                start_index = i;
            }
        }
    }

```



