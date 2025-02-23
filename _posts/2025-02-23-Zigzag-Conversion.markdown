---
layout: post
title: "Zigzag Conversion"
date: 2025-02-23
categories: jekyll update
---

[Check this out](https://leetcode.com/problems/zigzag-conversion/description/)

## Problem description

The string `PAYPALISHIRING` is written in a zigzag pattern on a given number 
of rows like this: (you may want to display this pattern in a fixed font for 
better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: `PAHNAPLSIIGYIR`

## Idea

When you finish reading the problem description section, many solutions might come to mind. 
However, for every problem, there is usually a core idea behind it.  
It's not about the code itself. Once you grasp the underlying idea, you’re good to go, and the code becomes secondary.

Look at this one, one more time `PAYPALISHIRING`

```
P   A   H   N
A P L S I I G
Y   I   R
```

You start to read `P` and then move down to read `A`, and continue down to read `Y`. 
Each time you move down, you’re progressing row by row —Row 1, Row 2, Row 3, and so on until Row n - 1
Row 1, 2 and 3 and so on until row n - 1. For each row, add the current character to the answer.
For each row, you add the current character to the answer.

Once you reach to the end of the road. You start moving back up,
So for this problem, you alternate between moving down and up, down and up and so on.
However, it's important to keep track of the current row and whether you need to go up or down.


For instance: ["", "", ""]. Push the current character to the first row:

```
["P", "", ""]
```

Move to the next character(Move down): 

```
["P", "A", ""]
["P", "A", "Y"]
```

At this point, you need to go up. 

```
["P", "AP", "Y"]
["PA", "AP", "Y"]
```

Just like this.

```rust
pub fn convert(s: String, num_rows: i32) -> String {
    if num_rows == 1 || s.len() <= num_rows as usize {
        return s;
    }

    // Keep track the current row
    let mut cur_row = 0;
    // Use to decide whether we need to move up or down
    let mut going_down = false;

    let mut rows: Vec<String> = vec![String::new(); num_rows as usize];

    for c in s.chars() {
        // Push the current character to the current row
        rows[cur_row].push(c);

        // When cur_row is 0, move down. Otherwise, move up
        if cur_row == 0 || cur_row == (num_rows - 1) as usize {
            going_down = !going_down;
        }
        // Continue move down
        if going_down {
            cur_row += 1;
        } else {
            // Continue move up
            cur_row -= 1;
        }
    }

    rows.concat()
}

```
