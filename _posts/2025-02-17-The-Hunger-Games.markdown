---
layout: post
title: "The Hunger Games - Zoo Disaster"
date: 2025-2-17
categories: jekyll update
---

[Check this out](https://www.codewars.com/kata/5902bc7aba39542b4a00003d/)

## Problem description

So, basically, there are some animals that are out of the cage. And they start to eat each other, but there are also rules in the following:

- Antelope eats grass.

- Big fish eat little fish.

- Bug eats leaves.

- bear eats big-fish

- Bear eats bug.

- Bear eats chicken.

- bear eats cow

- Bear eats leaves.

- Bear eats sheep.

- Chicken eats bug.

- Cow eats grass.

- Fox eats chicken.

- Fox eats sheep.

- Giraffe eats leaves.

- Lion eats antelope.

- Lion eats cow.

- panda eats leaves

- Sheep eat grass.


And you're given a list of animals, something like this:

``` 
"fox,bug,chicken,grass,sheep"
```

Reference to the constraints above, we see that `foxes` can't eat `bugs`, `bugs` can't eat `chickens`, but `chickens` can eat `bugs`, and so on…

## Working

| Step | Action                        | Remaining Items                     |
|------|-------------------------------|-------------------------------------|
| 1    | fox can't eat bug              | fox, bug, chicken, grass, sheep    |
| 2    | bug can't eat anything         | fox, bug, chicken, grass, sheep    |
| 3    | chicken eats bug               | fox, chicken, grass, sheep         |
| 4    | fox eats chicken               | fox, grass, sheep                  |
| 5    | fox can't eat grass            | fox, grass, sheep                  |
| 6    | grass can't eat anything       | fox, grass, sheep                  |
| 7    | sheep eats grass               | fox, sheep                         |
| 8    | fox eats sheep                 | fox                                |


| 💡                                                                                                             |
|----------------------------------------------------------------------------------------------------------------|
|  - Animals can only eat things beside them                                                                     |
|  - Animals always eat to their LEFT before eating to their RIGHT                                               |
|  - Always the LEFTMOST animal capable of eating will eat before any others                                     |
|  - Any other things you may find at the zoo (which are not listed above) do not eat anything and are not edible|


## Ideas to solve this problem

When looking at the **"Working"** section, we need a way to determine which animal can eat another. 
The first method that comes to mind is using a **hash map**. For example:

- **Fox** can eat **chicken** and **sheep**, so the hash map would look like this:

  ```
  Fox -> ["chicken", "sheep"]
  ```

In rust, I create a **hash map** like this:

```rust
    let mut zooz: HashMap<&str, Vec<&str>> = HashMap::with_capacity(11);

    zooz.insert("bear", Vec::from(["big-fish", "bug", "chicken", "cow", "leaves", "sheep"]));
    zooz.insert("antelope", Vec::from(["grass"]));
    zooz.insert("big-fish", Vec::from(["little-fish"]));
    zooz.insert("bug", Vec::from(["leaves"]));
    zooz.insert("chicken", Vec::from(["bug"]));
    zooz.insert("cow", Vec::from(["grass"]));
    zooz.insert("fox", Vec::from(["chicken", "sheep"]));
    zooz.insert("giraffe", Vec::from(["leaves"]));
    zooz.insert("lion", Vec::from(["antelope", "cow"]));
    zooz.insert("panda", Vec::from(["leaves"]));
    zooz.insert("sheep", Vec::from(["grass"]));
```

Pay your attention to the note; we need to explore its left first before we can explore its right.

For an example:

```
"fox,bug,chicken,grass,sheep"
```

We don't check if **chickens** can eat **grass** first, but we check if **chickens** can eat **bugs** first.

With that in mind, let's see from the list 

```
"fox,bug,chicken,grass,sheep"
```

**chicken** eats **bug**? Yes, so remove the **bug** from the list.

```
"fox,chicken,grass,sheep"
```

But there is a thing you need to consider very carefully. If you move your pointer that is currently pointing to the **chicken**, move it to the **grass** and check if the **grass** can eat **chicken**. That strategy will not work. You need to reset your pointer to the beginning of the list; that will point to the **fox**.


```rust
fn who_eats_who(zoo: &str) -> Vec<String> {
    let mut answer: Vec<String> = Vec::new();
    let mut zooz: HashMap<&str, Vec<&str>> = HashMap::with_capacity(11);

    zooz.insert("bear", Vec::from(["big-fish", "bug", "chicken", "cow", "leaves", "sheep"]));
    zooz.insert("antelope", Vec::from(["grass"]));
    zooz.insert("big-fish", Vec::from(["little-fish"]));
    zooz.insert("bug", Vec::from(["leaves"]));
    zooz.insert("chicken", Vec::from(["bug"]));
    zooz.insert("cow", Vec::from(["grass"]));
    zooz.insert("fox", Vec::from(["chicken", "sheep"]));
    zooz.insert("giraffe", Vec::from(["leaves"]));
    zooz.insert("lion", Vec::from(["antelope", "cow"]));
    zooz.insert("panda", Vec::from(["leaves"]));
    zooz.insert("sheep", Vec::from(["grass"]));

    let mut animals: Vec<&str> = zoo.split(",").collect();
    answer.push(animals.join(",")); // init
    let mut i = 0;

    while i < animals.len() {
        let animal = animals[i];
        // Explore its left
        if i > 0 {
            let left_animal = animals[i - 1]; // Get the left animal
            // See if there is animal in the map
            // If so, get the animals that it can eat
            if let Some(list_food) = zooz.get(animal) { 
                // If the left animal is the target of the current animal
                if list_food.contains(&left_animal) { 
                    // Remove the current that is eated by the current animal
                    let removed_animal = animals.remove(i - 1);
                    // Format the answer
                    answer.push(format!("{} eats {}", animal, removed_animal));
                    // Reset the pointer to the beginning of the list
                    i = 0; 
                    continue;
                }
            }
        }

        // explore right
        if i < animals.len() - 1 {
            let right_animal = animals[i + 1];
            if let Some(list_food) = zooz.get(animal) {
                if list_food.contains(&right_animal) {
                    let removed_animal = animals.remove(i + 1);
                    answer.push(format!("{} eats {}", animal, removed_animal));
                    i = 0; 
                    continue;
                }
            }
        }
        i += 1;
    }

    answer.push(animals.join(","));
    return answer;
```

Hope you enjoy it and have while coding.

