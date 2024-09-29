---
title: Python
---

# Python

## Footguns

- difference between `is` and `==`

## Tips and Tricks

- from time import sleep
- Open your current file in interactive mode to inspect/debug it
  `python -i file.py`
- String templating `print("%s : %s" % (name, age))`
- Pipenv environments are stored in `~/.local/share/virtualenvs`. Can be deleted as part of system cleanup

## Lists

`a = [1, 2, 3]

Python now has tools inspired from haskell to operate with lists in the module itertools. Documentation is [here](https://docs.python.org/3/library/itertools.html)

Use a list as stack

```python
stack = [2,3,4]
stack.append(5)
stack.append(6)
stack.pop()
stack.pop()
```

Use a list as Queue

```python
from collections import deque
queue = deque(["apple", "banana", "cat"])
queue.append("dog")
queue.append("elephant")
queue.popleft()
queue.popleft()
```

List Comprehensions
a concise way to create list

> A list comprehension consists of brackets containing an expression followed by a for clause, then zero or more for or if clauses. The result will be a new list resulting from evaluating the expression in the context of the for and if clauses which follow it.

List Display and Comprehension
`a = [x*x for x in range(10)]`

## Generators

If your function uses the yield command, its a generator.

```python
def natural_numbers():
    i = 0
    while True:
        yield i
        i ++
```

You can pass generators to functions as paramters by prefixing `*` to the parameter name - `def fun(*gen)`

Multiple ways to use iterators

- with a for loop

```python
    for num in natural_numbers:
        print(num)
```

inline usage

```python
  value = sum(next(t) for n in slice(natural_numbers, 10))
```

Use yield without a value

Simply writing the command yield, yields control to the calling code.

- Convert a generator into a context manager

```python
from contextlib import contextmanager

@contextmanager
def db_test(cur):
  cur.execute('create table points(x int, y int)')
  try:
    yield
  finally:
    cur.execute('drop table points ')
```

## Class

Special functions in a Class

- `__init__` : constructor
- `__repr__` : print your class sensibly
- `__add__` : operator overload the + operator
- `__iter__`, `__next__` : make the class iterable
  - raise StopIteration()
- `__enter__`, `__exit__` : make your class a ContextManger, with setup and teardown functions.

## Internals

- see what happens in the python bytecode

```python
from dis import dis
dis(function_name)
```

- inspect source code of a function in runtime

```python
from inspect import getsource
getsource(add)
```

# Ecosystem

- [Eventlet](http://eventlet.net/doc/index.html) brings concurrency to python

## References

- [So you want to be a python expert](https://www.youtube.com/watch?v=cKPlPJyQrt4) by James Powell
- [Transforming Code into Beautiful Idiomatic Python](https://www.youtube.com/watch?v=OSGv2VnC0go) by Raymond Hettinger
- Documentation for [Collections](https://docs.python.org/3/library/collections.html)
- An opinionated [guide](https://docs.python-guide.org/) to python

# Starting a new Python project

# Pipenv for package management and virtual environment

## Notes from Idiomatic Python

- ChainMap
- Clarify function calls with keyword arguments
  - You are sacrificing performance but improving developer time
- named tuples

```
from collections import namedtuple


def named_tuples(a: int):
    Results = namedtuple("Result", ["status", "payload"])
    if a < 0:
        return Results("error", {})
    if a > 0:
        return Results("success", {"number": a})


print(named_tuples(3))
print(named_tuples(-1))
```

- Updating Multiple state variables
- Decorators and Context Managers : Help separate business logic from administrative ones

# Async

Notes from [Keynote on Concurrency, PyBay 2017](https://www.youtube.com/watch?v=9zinZmE3Ogk)
Goal : When to use threads, processes, asyncs. Advantages and disadvantages

# Functional Programming

### Creating partial functions - [documenttion](https://docs.python.org/3/library/functools.html#functools.partial)

This reminds me of currying in haskell

```python
def user(name, age, role):
    return {"name":name, "age":age, "role":role}

manager = partial(user, role="manager")
admin   = partial(user, role="admin")

print(user(name="denny", age="32", role="user"))
print(manager(name="denny", age="38"))
print(admin(name="denny", age=42))
```

### Pattern and Matching

https://peps.python.org/pep-0636/
How to implement delegation using pattern matching

Requires python 3.10+

```python
action_pass = {"type": "pass", "payload": {"name": "denny"}}
action_keep = {"type": "keep", "payload": {}}

action = action_pass

match action:
    case {type, payload}:
        print(type)
```

## Live Development Process with Reload

Uses the inotify syscall on linux to trigger reload of the program upon file changes

![Cli Gif](/python-live-reload.gif)

```python
import inotify.adapters
import subprocess

def watch():
    i = inotify.adapters.Inotify()

    i.add_watch('./')

    for event in i.event_gen(yield_nones=False):
        (_, type_names, path, filename) = event

        #print("PATH=[{}] FILENAME=[{}] EVENT_TYPES=[{}]".format(path,filename,type_names))
        for type in type_names:
            #print("type: {} path: {} filename: {}".format(type, path, filename))
            if type == "IN_CLOSE_WRITE" and ".py" in filename:
                print('reload file')
                subprocess.run(["python", "hello.py"])

if __name__ == '__main__':
    watch()
```

# Numerical and Scientific Computing

```python
import numpy as np
import plotly.express as px

x = np.linspace(-np.pi, np.pi, 50)
y = np.array([np.sin(i) for i in x])
fig = px.scatter(x=x, y=y)
fig.show()
```

![numpy simple plot](../../images/plotly-numpy-101.png)

- [Statistics](https://numpy.org/doc/stable/reference/routines.statistics.html)
- [Randomness](https://numpy.org/doc/stable/reference/random/index.html)
- [Maths](https://numpy.org/doc/stable/reference/routines.math.html)
- [Logic](https://numpy.org/doc/stable/reference/routines.logic.html)
- [Linear Algebra](https://numpy.org/doc/stable/reference/routines.logic.html)

SciPy, Pandas and OpenCV use numpy array as the common format for data exchange
