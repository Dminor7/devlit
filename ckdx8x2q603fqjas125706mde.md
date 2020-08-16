## [Python] Part 1 Generator: Introduction

# Generator

Before starting with what generators are, we’ll first discuss what iteration, iterables, and iterators are.

## Iteration

Iteration is a term for taking each item of something, one after another. Any time you use a loop, explicit or implicit, to go over a group of items, that is iteration.

## Iterable
  
Iterable is an object that is, well, iterable, which simply means that it can be used in iteration, e.g. with a for loop. How? By using an iterator. I'll explain it below. Iterable objects also define `__iter__` that returns an iterator and also have a `__getitem__` method suitable for indexed lookup. Examples of iterables include lists, tuples, and strings - any such sequence that can be iterated over a loop.

## Iterator
  
An iterator is an object that defines how to actually do the iteration, specifically what is the next element. That's why it must have the `next()` method. It remembers where it is during iteration.

### Let’s look an example to clarify things up:

```python
>>> # ranks is an iterable
>>> ranks = [1,2,3]

>>> # Returns True ranks has __iter__ method
>>> __iter__ in dir(ranks)
True
>>> # Returns True ranks has __getitem__ method
>>> __getitem__ in dir(ranks)
True

>>> # ranks is now an iterator
>>> ranks = iter(ranks)
>>> # Retuns True ranks has __next__ method
>>> __next__ in dir(ranks)
True
>>> next(ranks)
1
>>> next(ranks)
2
>>> next(ranks)
3
>>> # next() raises StopIteration, to signal that iteration is complete
>>> next(ranks)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```
Whenever we use a `for` loop, or `map`, or a `list comprehension`, etc. in Python, the next method is called automatically to get each item from the iterator, thus going through the process of iteration.

With our knowledge of iterators, we can implement the evaluation rule of a `for` statement in terms of while, assignment, and try statements.

```python
>>> i = ranks.__iter__() # or iter(ranks)
>>> try:
        while True:
            item = i.__next__() # or next(i)
            print(item)
    except StopIteration:
        pass
1
2
3
```
In the above example if we want to keep track of our iteration we need to introduce a new field `current` to keep track of progress through the sequence. With simple sequences like one shown above, this can be done easily. With complex sequences, however, it can be quite difficult for the `next()` function to save its place in the calculation. Hence, comes `generators` allowing us to define more complicated iterations.

## What is a generator?

A generator is an iterator returned by a special class of function called a generator function. Generator functions are distinguished from regular functions in that rather than containing return statements in their body, they use yield statement to return elements of a series.

```python

>>> def countdown(n): 
        while n > 0: 
            yield n 
            n -= 1 
>>> for i in countdown(5):
        print(i, end=' ')

5 4 3 2 1

```

Above, the behavior is different from normal functions. Calling a generator function creates a generator object.

```python

>>> def countdown(n): 
        while n > 0: 
            yield n 
            n -= 1 
>>> c = countdown(5)
<generator object countdown at 0x0000017CD6788360>

```

***The function only executes on next()***

```python

>>> next(c)
5
>> >next(c)
4
# and so on until next() raises StopIteration

```

A generator is kinda different from objects that support iteration. We can iterate over the generated data once, but if we want to do it again, we have to call the generator function again (resetting generator).

Like list comprehensions, generators also support concise notions for such operations. Using `‘()’ `

```python
>>> gen = (expression for i in s if condition)
```

**Note**: In the above countdown example it doesn’t start running the function. It only computes when we request for data (The technical term for this behavior is `lazy evaluation`). Therefore not loading everything at once in in-memory is a useful perk of generators that we can exploit while dealing with a `huge amount of data`. We can model sequences with `no definite` end using generators

### Below is an example of an `infinite` sequence of even numbers

```python
>>> def infinte_range(step):
        i = 0
        while True:
            yield i
            i += step
>>> even_numbers = (x for x in infinte_range(2))
>>> next(even_numbers)
0
>>> next(even_numbers)
2
>>> next(even_numbers)
4
>>> next(even_numbers)
6
```

