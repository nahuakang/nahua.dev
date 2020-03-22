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
### Everything in Python is an Object
In Python, everything is an object. So when you see an integer `1` or a string `'hello'`, they are objects, too. Just try typing `type(0)` or `type('a')`:
```python
>>> type(1)
<class 'int'>
>>> type('a')
<class 'str'>
```
They are instances of the class integer and the class string.

### What Variable Assignment Really Is
Going a step further, when we declare a variable `a = 1`, the variable itself does not really hold the value `1`. Instead, the variable is a *reference* to a value that is an integer object `1`, which is an instance of the integer class.

If this sounded a bit abstract, try think of the integer `1` as if it existed in the Python universe all along, with its own address in this universe. When we declare `a = 1`, we have simply created a name to point to this integer as a reference.

In a way, we could create many names for the integer `1`. Let's try playing with the integer object `1` inside the Python console a bit:
```python
>>> id(1)     # The address where integer value 1 lives in
4362298512
>>> a = 1
>>> id(a)     # The address of the value that variable 'a' points to
4362298512
>>> b = a     # Assign 'b' to the same value that 'a' points to
>>> id(b)     # The address that 'b' points to is the same that 'a' points to
4362298512
```
As you can see, the integer `1` has its own address (the exact address will most certainly differ in the universe of your computer), in this case, `4362298512`. If we assigned variable `a` to the integer object `1`, we merely declared a *noun* that references the address of `1`.

When we then declared another variable `b` to the variable `a`, we are literally telling Python to let the variable `b` be a reference to the same value that `a` is pointing to, which is the integer object `1`.

### Variable Reassignments
Let's dig deeper. If we perform the operation `a = a + 1`, we do not increase the integer value at the address, which in this case is `4362298512`. Instead, we are pointing the variable `a` to a new value `2`.

```python
>>> a = a + 1 # What happens if we add 1 to the variable 'a'?
>>> id(a)     # 'a' points to a new address
4362298544
>>> id(2)     # which is the same address that integer 2 lives on
4362298544
>>> id(1)     # Integer 1 still lives on its own address
4362298512
>>> id(b)     # 'b' still points to integer 1
4362298512
```

## Const in Javascript

