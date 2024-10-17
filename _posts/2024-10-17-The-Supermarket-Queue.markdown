---
layout: post
title: "The Supermarket Queue"
date: 2024-10-17
categories: jekyll update
---

# The Supermarket Queue

[check this out](https://www.codewars.com/kata/57b06f90e298a7b53d000a86/train/rust)

There is a queue for the self-checkout tills at the supermarket. Your task is write a function to calculate the total time required for all the customers to check out!

## Input

- customers: an array of positive integers representing the queue. Each integer represents a customer, and its value is the amount of time they require to check out.
- n: a positive integer, the number of checkout tills.

## Output

The function should return an integer, the total time required.

# Example

Look at this array: queueTime([10,2,3,3], 2). There are 2 cashiers, and 4 customers (length of the array). 
The first person has 10 items, the second person has 2 items and so on. So, imagine you entered a supermarket and waiting for check out,
there are 2 cashiers in this supermarket. The first person takes the first crashier and he has 10 items to check out, the second person is 
standing at the second crashier with only 2 items. Which one will be checking out faster? Of course, the person who has 2 items will be left sooner. 
So you will queue behind the second person at crashier number 2.

| 1 | 2 | 
|----------|----------|
| 10 | 2 |
| _ | 3 |
| _ | 3 |

and the total is max(10, 2+3+3) that is 10. That's it.

```rust
pub fn queue_time(customers: &[u32], n: u32) -> u32 {
    let mut n_vec: Vec<u32> = vec![0; n as usize];

    for &customer in customers {
        let min_index = n_vec.iter().enumerate().min_by_key(|&(_, &val)| val).unwrap().0;
        n_vec[min_index] += customer;
    }

    *n_vec.iter().max().unwrap()
}
```

Just create an array with n number, init it with 0.
Find the min index of its and from this add more to that position like we did ini the table above.


