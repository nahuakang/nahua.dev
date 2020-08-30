---
title: "Python: Immutables Are Not Always Immutable"
date: 2020-03-22T11:05:25+01:00
draft: false
toc: false
images:
tags: [python, oop, immutability, mutability]
---

If you know a bit of Python, you probably have heard of *immutable* and *mutable* objects (see [data model](https://docs.python.org/3.8/reference/datamodel.html)). Objects can either be mutable or immutable, depending on which type they are.

## Immutables and Mutables: Basics
First, let's review the basics of immutables and mutables that we all know.

### Mutable Objects
Mutable ones can be changed after they are created. For Python, collections like `list`, `dict`, and `set` are mutable objects. If we create a list, we can change its elements.

```python
>>> lst = ["list",  "objects",  "are", "immutable?"]
>>> lst
["list",  "objects",  "are", "immutable?"]
>>> lst[-1] = "mutable!"
>>> lst
["list",  "objects",  "are", "mutable!"]
```

### Immutable Objects
Immutable objects cannot be changed after creation. `bool`, `int`, `float`, `str`, `frozenset`, and `tuple` are immutable. So we will get an error if we attempt to reassign a tuple:

```python
>>> t = (1, 2)
>>> type(t)
<class 'tuple'>
>>> t[1]
2
>>> t[1] = 3
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

Try create a variable that references to a string object, such as `string = 'hello'`. If you attempted to reassign one element of the string (`string[1] = 'h'`), Python console would throw the same `TypeError`.

### Slightly Trickier Objects
If `tuple` is immutable and `list` is mutable, what about a tuple of lists then? Is a tuple like `([1, 2], [3, 4])` mutable or immutable?

```python
>>> tulip = ([1, 2], [3, 4])    # Create a tuple of two lists
>>> tulip
([1, 2], [3, 4])
>>> tulip[0] = [5, 6]           # Attempt to change the element results in error
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
>>> tulip[0][0] = 0             # Changing element of the list itself works
>>> tulip
([0, 2], [3, 4])
```


## Immutables and Mutables: Dive Deeper
As you can see, the story is a little bit more complicated. On the one hand, we cannot reassign an element of the tuple because tuples are immutable. On the other hand, we can reassign an element of a list inside a tuple, because lists are mutable.

To understand this topic better, we can go deeper into the knitty gritties of Python.

### Everything in Python is an Object
In Python, everything is an object. So when you see an integer `1` or a string `'hello'`, they are objects, too. Just try typing `type(0)` or `type('a')`:
```python
>>> type(1)
<class 'int'>
>>> type('a')
<class 'str'>
```
They are instances of the class integer and the class string.

### Refining Our Definition of Object Mutability
For an object in memory, it might contain information such as its object type and some data. In the realm of Python, changing the data inside an object is called modifying the ***internal state*** of this object. If we change the data inside an object and the object's memory address has not changed, the object is ***mutated***.

So now we can refine our definition of Python objects' mutability:

- An object whose internal state can be changed is a ***mutable***.
- An object whose internal state cannot be changed is an ***immutable***.

### Immutables
As we discussed, numbers (`int`, `float`, `booleans`, etc.), strings, and tuples are immutables. An integer object, could contain the information of the type `class 'int'` and a value of `1`.
```python
>>> type(1)
<class 'int'>
```

When we declare a variable `a = 1`, the variable itself does not really hold the value `1`. Instead, the variable is a *reference* to a value that is an integer object `1`, which is an instance of the integer class.

```python
>>> a = 1
```

If this sounded a bit abstract, try think of the integer `1` as if it existed in the Python universe all along, with its own address in this universe. When we declare `a = 1`, we have simply created a name to point to this integer as a reference.

In a way, we could create many names for the integer `1`. Let's try playing with the integer object `1` inside the Python console a bit:
```python
>>> id(1)     # The address where integer value 1 lives in
4362298512
>>> id(a)     # The address of the value that variable 'a' points to
4362298512
>>> b = a     # Assign 'b' to the same value that 'a' points to
>>> id(b)     # The address that 'b' points to is the same that 'a' points to
4362298512
```

As you can see, the integer `1` has its own address (the exact address will most certainly differ in the universe of your computer), in this case, `4362298512`. If we assigned variable `a` to the integer object `1`, we merely declared a *noun* that references the address of `1`.

When we then declared another variable `b` to the variable `a`, we are literally telling Python to let the variable `b` be a reference to the same value that `a` is pointing to, which is the integer object `1`.

Let's dig deeper. If we perform the operation `a = a + 1`, we do not change the value of this integer object at the memory address of `4362298512`. Instead, Python creates another integer object with value `2`, to which we now point the variable `a`.

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

You probably realized it already: We cannot alter the internal state of the integer object 1. It is immutable. When we do `a = a + 1`, we create a new integer object `2` and re-point our variable name `a` to `2` instead of incrementing the value of `1` by 1.


### Mutables
Let's create a class in Python called `Person`:
```python
class Person:
    def __init__(self, first_name, last_name, age):
        self.first_name = first_name
        self.last_name = last_name
        self.age = age
```

A `Person` object could contain the type `class '__main__.Person'`with additional data such as `first_name`, `last_name`, and `age`.
```python
>>> nahua = Person("Nahua", "Kang", 29)
>>> type(nahua)
<class '__main__.Person'>
>>> isinstance(nahua, Person)
True
>>> nahua.first_name
'Nahua'
>>> nahua.last_name
'Kang'
>>> nahua.age
29
```

We can go so far as to check up the address that the object `nahua` resides on in memory and see if we can alter the data inside the object:
```python
>>> id(nahua)
4374562064
>>> nahua.first_name = "nashua"
>>> id(nahua)
4374562064
```

## Immutable of Mutables

Coming back to our original, tricky example:
```python
>>> tulip = ([1, 2], [3, 4])    # Create a tuple of two lists
>>> tulip
([1, 2], [3, 4])
>>> id(tulip)
140313768890112
>>> id(tulip[0])
140313769534800
>>> id(tulip[1])
140313768720576
```

Notice that a `tuple` is immutable. So we have assigned the variable `tulip` to a tuple whose internal state contains two `lists`, each with a specific ID address. 

```python
>>> tulip[0] = [5, 6]           # Cannot re-assign one element of an immutable to a new object
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

If we try to re-assign the first list of our tuple `tulip` to another list object, which has a different ID address, that would not work. This is because the tuple is **immutable**, as in we cannot change the ID addresses of the elements in its internal state.


```python
>>> tulip[0][0] = 5   # But that element, which is mutable, can change its elements
>>> tulip
([5, 2], [3, 4])
>>> id(tulip[0])      # The first list object's ID is not changed
140313769534800       # which means we did not modify the internal state of an immutable
```

However, each of its two list objects is **mutable**, which means that we can modify their internal states legally. This is why we could modify the mutable inside an immutable.

## The End

While in most cases, Python immutables are immutable and mutables are mutable. But in some cases we'd run into immutables that contain mutable elements and it would be important to know when these cases occur. The rule of thumb is to understand the relationship between the ID of an object and the IDs of its elements in relationship to the object's type and mutability/immutability.

Hopefully this post helps you a bit. Happy programming in Python :)