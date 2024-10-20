---
layout: post
title: "Hidden "Cubic" numbers"
date: 2024-10-20
categories: jekyll update
---

# Hidden "Cubic" numbers

[check it out](https://www.codewars.com/kata/55031bba8cba40ada90011c4)

## Description

We search non-negative integer numbers, with at most 3 digits, such as the sum of the cubes of their digits is the number itself; we will call them "cubic" numbers.

    153 is such a "cubic" number : 1^3 + 5^3 + 3^3 = 153

These "cubic" numbers of at most 3 digits are easy to find, even by hand, so they are "hidden" with other numbers and characters in a string.

The task is to find, or not, the "cubic" numbers in the string and then to make the sum of these "cubic" numbers found in the string, if any, and to return a string such as:

"number1 number2 (and so on if necessary) sumOfCubicNumbers Lucky" 

if "cubic" numbers number1, number2, ... were found.

The numbers in the output are to be in the order in which they are encountered in the input string.

If no cubic numbers are found return the string: `"Unlucky"``.

## Example
``` 
- s = "aqdf&0#1xyz!22[153(777.777" 
   the groups of at most 3 digits are 0 and 1 (one digit), 22 (two digits), 153, 777, 777 (3 digits)
   Only 0, 1, 153 are cubic and their sum is 154
   Return: "0 1 153 154 Lucky"

- s = "QK29a45[&erui9026315"
  the groups are 29, 45, 902, 631, 5. None is cubic.
  Return: "Unlucky"
```

## Work through

To be honest, this one is so difficult for me but it's very interesting to solve.

Given a string like: `aqdf&0#1xyz!22[153(777.777`. And we want to find the number in this string and group it to most 3 digits:

    `["0", "1", "22", "153", "777", "777"]`

After that, for each element in this array, we want to find the cube number. For example, in the array we have element `153`:

`1^3 + 5^3 + 3^3 = 153` and that is the cube number.

We calculate if a given number is a cube number like this: 

```rust
fn sum_of_cubic_number(num: i32) -> bool {
    let s = num.to_string();
    let mut t: Vec<i32> = Vec::new();

    for c in s.chars() {
        if let Ok(mut j) = c.to_string().parse::<i32>() {
            j = j.pow(3);
            t.push(j);
        }
    }
    let sum = t.iter().sum::<i32>();
    if sum == num {
        return true;
    }

    false 
}
```

But how do we from `aqdf&0#1xyz!22[153(777.777` to `["0", "1", "22", "153", "777", "777"]`? 

```rust
use regex::Regex;

fn extract_digit_to_groups(s: &str) -> Vec<&str> {
    let re = Regex::new(r"\d+").unwrap();
    re.find_iter(s).map(|mat|mat.as_str()).collect()
}
```

In the code above, we use `Regex` to filter the number in the given string.
In solving problem, there are so many cases we need to consider. 

How about this string `00 9026315 -827&()`? With the code uses the regex above, we get this: 
`["00", "9026315", "827"]` but this is not what we wanted. We want this:
`["00", "902", "631", "5", "827"]`.

And to divide it to at most 3 digits:

```rust
    let mut arr_with_3_digits: Vec<String> = Vec::new();

    for i in ts.iter() {
        let chars: Vec<char> = i.chars().collect();
        for chunk in chars.chunks(3) {
            arr_with_3_digits.push(chunk.iter().collect());
        }
    }
```

And here is the entire code:

```rust
extern crate regex;
use regex::Regex;

fn extract_digit_to_groups(s: &str) -> Vec<&str> {
    let re = Regex::new(r"\d+").unwrap();
    re.find_iter(s).map(|mat|mat.as_str()).collect()
}

fn sum_of_cubic_number(num: i32) -> bool {
    let s = num.to_string();
    let mut t: Vec<i32> = Vec::new();

    for c in s.chars() {
        if let Ok(mut j) = c.to_string().parse::<i32>() {
            j = j.pow(3);
            t.push(j);
        }
    }
    let sum = t.iter().sum::<i32>();
    if sum == num {
        return true;
    }

    false 
}

fn is_sum_of_cubes(s: &str) -> String {
    let mut answer = String::new();
    let ts = extract_digit_to_groups(s);

    let mut arr_with_3_digits: Vec<String> = Vec::new();

    for i in ts.iter() {
        let chars: Vec<char> = i.chars().collect();
        for chunk in chars.chunks(3) {
            arr_with_3_digits.push(chunk.iter().collect());
        }
    }

    for j in arr_with_3_digits.iter() {
        let b = sum_of_cubic_number(j.parse::<i32>().unwrap());
        if b {
            if j.len() == 2 && j.chars().nth(0) == j.chars().nth(1) {
                answer.push(j.chars().nth(0).unwrap());
            } else {
                answer.push_str(j);
            }
            answer.push_str(" ");
        }
    }
    if answer.len() > 0 {
        let sum: i32 = answer.split_whitespace().map(|x| x.parse::<i32>().unwrap()).sum();
        answer.push_str(&sum.to_string());
        answer.push_str(" Lucky");
    } else {
        answer.push_str("Unlucky");
    }

    answer
}
```

