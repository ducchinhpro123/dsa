---
layout: post
title: Zero Matrix
date: 2024-12-5
categories: jekyll update
---

# Problem

Zero Matrix: Write an algorithm such that if an element in an MxN matrix is 0, its entire row and 
column are set to 0. 

# Discussion

Does it sound easy to you? In a matrix, if you encountered a 0 number then you need to set 
its row and its column to zero. For example

```
1 2 3  |  1 2 0
4 5 0  |  0 0 0
7 8 9  |  7 8 0
```

![matrix](/dsa/assets/images/matrix-example.png)

The first one is the original matrix, and the second is the output. But let's imagine that if you encountered a number 0
Then you start to fill 0 in its row and column, and then you continue, but you still encounter number 0 at the end. 
and you may end up with filling the entire last row with number 0 too. So you need a way to mark it.

```java
    void zeroMatrix(int[][] matrix) {
        boolean rows[] = new boolean[matrix.length];
        boolean cols[] = new boolean[matrix[0].length];
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                if (matrix[i][j] == 0) {
                    rows[i] = true;
                    cols[j] = true;
                }
            }
        }

        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                if (rows[i] || cols[j]) {
                    matrix[i][j] = 0;
                }
            }
        }
    }
```
