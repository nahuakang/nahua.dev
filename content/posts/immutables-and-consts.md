---
title: "Immutables Are Not Always Immutable"
date: 2020-02-22T11:05:25+01:00
draft: false
toc: false
images:
tags:
  - untagged
---


## Immutables in Python
In Python, everything is an object. 

When we declare a variable `a = 1`, the variable itself does not really hold the value `1`. Instead, the variable is a reference to an integer object `1`.

If this sounded a bit abstract, try think of the integer `1` as if it existed in the Python universe all along, with its own address in this universe. When we declare `a = 1`, we have simply created a name to point to this integer as a reference.

In a way, we could create many names for the integer `1`. Let's try playing with the integer object `1` inside the Python console a bit:
```python
>>> id(1)
4362298512
>>> a = 1
>>> id(a)
4362298512
>>> b = a
>>> id(b)
4362298512
```

## Const in Javascript

