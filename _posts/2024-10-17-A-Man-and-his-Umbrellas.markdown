---
layout: post
title: "A Man and his Umbrellas"
date: 2024-10-17
categories: jekyll update
---

# A Man and his Umbrellas

[check this out](https://www.codewars.com/kata/58298e19c983caf4ba000c8d)

Each morning a man walks to work, and each afternoon he walks back home.

If it is raining in the morning and he has an umbrella at home, he takes an umbrella for the journey so he doesn't get
wet, and stores it at work. Likewise, if it is raining in the afternoon and he has an umbrella at work, he takes an
umbrella for the journey home.

## Input

The input is an array/list of consecutive half-day weather forecasts. So, e.g. the first value is the 1st day's morning
weather and the second value is the 1st day's afternoon weather. The options are:

Without umbrella:

    "clear",
    "sunny",
    "cloudy",
    "overcast",
    "windy".

With umbrella:

    "rainy",
    "thunderstorms".

## Output

minimum number of umbrellas

## Example

`minUmbrellas(["rainy", "clear", "rainy", "cloudy"])`

should return 2

Because on the first morning, he needs an umbrella to take, and he leaves it at work. So on the second morning, he needs
a second umbrella.

## Imagine

Imagine is always a fun part of any problem. So, let's say we have an array like this:

`minUmbrellas(["rainy", "clear", "rainy", "cloudy"])`

The first and the second value is this array is in one day: the day the man goes to work at the morning
and the day he goes back home at afternoon.

Look at the array again, we see that the on the first day morning, it's `rainy` so he needs to bring an
umbrellas, when he goes back it's `clear`, so he leaves the umbrellas at work. On the second day morning,
it's `rainy` again and `cloudy` when he leaves. So how many umbrellas has take? That is 2. 

So you get the idea.

## Code
```rust
fn min_umbrellas(weather: &[&str]) -> usize {
    let mut i = 0;
    let mut total_umbrellas = 0;
    let mut umbrellas_home = 0;
    let mut umbrellas_work = 0;

    while i < weather.len() {
        // Start of the day
        if i % 2 == 0 && (weather[i] == "rainy" || weather[i] == "thunderstorms") {
            if umbrellas_home > 0 {
                umbrellas_home -= 1;
            } else {
                total_umbrellas += 1;
            }
            umbrellas_work += 1;
        // End of the day
        } else if i % 2 == 1 && (weather[i] == "rainy" || weather[i] == "thunderstorms") {
            if umbrellas_work > 0 {
                umbrellas_work -= 1;
            } else {
                total_umbrellas += 1;
            }
            umbrellas_home += 1;
        }
        i += 1;
    }

    total_umbrellas
}
``` 
The code is pretty simple. It just tells us that _Did he take the umbrellas at work when it's raining?_
