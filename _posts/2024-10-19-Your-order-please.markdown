---
layout: post
title: "Your order! please"
date: 2024-10-19
categories: jekyll update
---

# Your order! please

[check this out](https://www.codewars.com/kata/55c45be3b2079eccff00010f)

## Description

Your task is to sort a given string. Each word in the string will contain a single number. This number is the position the word should have in the result.

Note: Numbers can be from 1 to 9. So 1 will be the first word (not 0).

If the input string is empty, return an empty string. The words in the input String will only contain valid consecutive numbers.


## Examples

```
"is2 Thi1s T4est 3a"  -->  "Thi1s is2 3a T4est"

"4of Fo1r pe6ople g3ood th5e the2"  -->  "Fo1r the2 g3ood 4of th5e pe6ople"
""  -->  ""
```

## Work through

So, basically we need to sort the given string in order based on its number.
Consider this given string: `is2 Thi1s T4est 3a`, so we need a way to seperate it into the array like this: 
`["is2", "Thi1s", "T4est", "3a"]`. After that, we loop through this array and check if we encounter a number then add this 
number to something like: `2: is2` and so on...

So what else do we got in here? if we can see this:

```
2: is2,
1: Thi1s,
4: T4est,
3: 3a
```

And that's right, that's _hashmap_, our best friend. But we have a problem in here, the map isn't sorted. Fotunately, we got
[B-Tree](https://en.wikipedia.org/wiki/B-tree). And `BTreeMap`, which is based on `B-tree` and also hashmap but sorted by default. So we have: 

```
1: Thi1s,
2: is2,
3: 3a
4: T4est,
```

And then just add these values into the string.

```rust
use std::collections::BTreeMap;

fn order(sentence: &str) -> String {
    let sentence_array: Vec<&str> = sentence.split_whitespace().collect();
    let mut map: BTreeMap<u32, &str> = BTreeMap::new();
    let mut answer = String::new();

    for i in 0..sentence_array.len() {
        for j in sentence_array[i].chars() {
            if j.is_numeric() {
                map.insert(j.to_digit(10).unwrap_or(0), sentence_array[i]);
                break
            }
        }
    }

    for value in map.values() {
        answer.push_str(value);
    }

    answer
}
```


