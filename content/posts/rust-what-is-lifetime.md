---
title: "Rust What Is Lifetime"
date: 2020-09-13T13:48:37+02:00
draft: true
toc: false
images:
tags:
  - untagged
---

@bobahop on Exercism:

You're very welcome!

As for lifetimes...a HashSet of str references is being returned. They can't be references to str values created in anagrams_for, since those values would go out of scope and be destroyed at the end of the anagrams_for function. So they need to reference something being passed in. The HashSet is populated by references to the values in possible_anagrams, so we have to specify to the compiler that we are sure that the lifetime of the values referenced in the return HashSet is as long as for the values referenced in possible_anagrams.

The common idiom of using 'a doesn't really help to understand. This might make it clearer...
```rust
pub fn anagrams_for<'possible_anagrams_lifetime>(word: &str, possible_anagrams: &[&'possible_anagrams_lifetime str]) -> HashSet<&'possible_anagrams_lifetime str> {}
```
It's way more verbose, which is why it's not done, but it may help to make it clearer what we're telling the compiler. If we were not passing in word: &str then [lifetime elision] would allow us to omit all of the specified lifetimes, as we then wouldn't have to tell the compiler if the output referenced word or possible_anagrams.

Of course, we can't return `HashSet<str>` because, as the compiler tells us, it can't determine the length of the str at compile time.

So, another way to do this would be return a heap-allocated object whose size of its pointer on the stack is known. This won't be accepted by the tests, but in the world one could do...
```rust
pub fn anagrams_for(word: &str, possible_anagrams: &[&str]) -> HashSet<String> {
...
anagrams.insert(possibility.to_string());
```
For just a few values it's not a big deal, but if we were dealing with a lot of values we would want the performance of keeping them references and leading the compiler by the hand by the lifetime annotations.

You might be interested in a [detailed description of lifetimes]. It's somewhat long and it takes a while before it starts getting very interesting, but by the end you may think it's been worth the time reading it.
