---
layout: post
title: Duplicate Encoder
date: 2024-10-21
categories: jekyll update
---

# Duplicate Encoder

[check it out](https://www.codewars.com/kata/54b42f9314d9229fd6000d9c)

## Description

The goal of this exercise is to convert a string to a new string where each character in the new string is
"(" if that character appears only once in the original string, or ")" if that character appears 
more than once in the original string. Ignore capitalization when determining if a character is a duplicate.

## Example

``` 
"din"      =>  "((("
"recede"   =>  "()()()"
"Success"  =>  ")())())"
"(( @"     =>  "))((" 
```

## Work through

There is a way to solve this exercise is that to use _HashMap_. 

This one is quite simple. It's just like this:

```
let answer is String
for word in words:
    int count = hashmap.get(word)
    if count == 1:
        append "(" to `answer`
    else:
        append ")" to `answer`
```

## Code

```rust
use std::collections::HashMap;

fn duplicate_encode(word:&str)->String {
    let mut answer = String::new();
    let mut map: HashMap<char, u32> = HashMap::new();

    // If the word already in the map, increment the value by 1
    // Else the default value of the key word is 1 
    for i in word.to_lowercase().chars() {
        let c = map.entry(i).or_insert(0);
        *c += 1;
    }

    for i in word.to_lowercase().chars() {
        let ocur_number = map.get(&i).unwrap();
        // The word that only occurs only one
        if ocur_number == &1 {
            answer.push_str("(");
        } else { // The word that occurs more than one
            answer.push_str(")");
        }
    }

    answer
}
```

