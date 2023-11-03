---
title: "Python 3.11 Release - What you should know"
author: Shana
keywords: [no, nothing]
date: 2022-10-28
---

Python 3.11 was released on Oct. 24th, 2022. This latest version makes Python faster and even more user-friendly. If you’re not ready to take the time to read the full official [“What’s New” doc](https://docs.python.org/3/whatsnew/3.11.html), I've got you covered. Here are the top 5 things you should know about the Python 3.11 release, including handy code samples.

## 1. It's Faster

Compared to Python 3.10, 3.11 is fast. Really fast.

One way you can see this for yourself is by using the [pyperformance](https://pyperformance.readthedocs.io/) tool. `pyperformance` is the standard performance measuring tool that CPython uses to validate their changes. Here’s one benchmark from that suite: `django_template`.

### Run in Python 3.10

```bash
virtualenv venv310 -ppython3.10
./venv310/bin/pip install pyperformance
./venv310/bin/pyperformance run -b django_template
```

```output
Python benchmark suite 1.0.5

==================================================
( 1/1) creating venv for benchmark (django_template)

...

Performance version: 1.0.5
Python version: 3.10.8 (64-bit)
Report on macOS-12.6-arm64-arm-64bit
Number of logical CPUs: 10
Start date: 2022-11-04 15:38:56.714169
End date: 2022-11-04 15:39:10.918179

### django_template ###
Mean +- std dev: 27.7 ms +- 0.6 ms
```

We can see that this ran for ~28 ms on my machine.

### Run in Python 3.11

```bash
virtualenv venv311 -ppython3.11
./venv311/bin/pip install pyperformance
./venv311/bin/pyperformance run -b django_template
```

```output
Python benchmark suite 1.0.5

==================================================
( 1/1) creating venv for benchmark (django_template)

...

Performance version: 1.0.5
Python version: 3.11.0 (64-bit) revision deaf509e8f
Report on macOS-12.6-arm64-arm-64bit
Number of logical CPUs: 10
Start date: 2022-11-04 15:52:40.979797
End date: 2022-11-04 15:53:01.172844

### django_template ###
Mean +- std dev: 21.1 ms +- 0.6 ms
```

And the new version ran for ~21 ms.

This very unscientific test shows about a ~25% speedup, which lines up very nicely with the [reported average 25% speedup](https://docs.python.org/3/whatsnew/3.11.html#faster-cpython), but your mileage may vary.

## 2. New `tomllib` library

The new [`tomllib` library](https://docs.python.org/3/library/tomllib.html#module-tomllib) brings support for parsing [TOML](https://toml.io/en/) files. `tomllib` does not support writing TOML. It's based on the [`tomli`](https://github.com/hukkin/tomli) library.

The two main functions in `tomllib` are:

- `load()`: load bytes from file
- `loads()`: load from `str`

Here's an example of each:

```python
import tomllib

# gives TypeError, must use binary mode
with open('t.toml') as f:
    tomllib.load(f)

# correct
with open('t.toml', 'rb') as f:
    tomllib.load(f)

# correct
with open('t.toml') as f:
    tomllib.loads(f.read())

# gives TypeError, can't read bytestring
with open('t.toml', 'rb') as f:
    tomllib.loads(f.read())
```

## 3. `asyncio` Task and Exception Groups

[Task groups](https://docs.python.org/3/library/asyncio-task.html#task-groups) are conceptually similar to the [`concurrent.futures` module](https://docs.python.org/3/library/concurrent.futures.html) and what they did for the [`multiprocessing` module](https://docs.python.org/3/library/multiprocessing.html). They give you a convenient executor to run multiple tasks and join them together at the end.

Task groups can be a replacement for [`asyncio.gather()`](https://docs.python.org/3/library/asyncio-task.html#running-tasks-concurrently).

Here's an example of what using `asyncio.gather()` looks like:

```python
import asyncio

async def f1(x: int) -> None:
    await asyncio.sleep(x / 10)
    print(f'hi from {x}')

async def amain() -> int:
    # clunky, previous way of doing this
    futures = [f1(i) for i in range(5)]
    await asyncio.gather(*futures)
    print('done')
    return 0

def main() -> int:
    return asyncio.run(amain())

if __name__ == '__main__':
    raise SystemExit(main())
```

This is clunky and doesn't give you the flexibility to call other functions or use loops or conditions, because all the futures must be gathered in one place.

Task groups make this much easier:

```python
...

async def amain() -> int:
    # new, nice way of doing this!
    async with asyncio.TaskGroup() as tg:
        # you can do loops, conditions, etc
        for i in range(5):
            tg.create_task(f1(i))

    print('done')
    return 0

...
```

The task group causes all tasks to run to completion before the context exits, giving you much more flexibility.

## 4. Improvements to Exceptions

There's a lot here, so I'm going to split this up into sections:

### Exception groups

First up are [exception groups](https://docs.python.org/3/whatsnew/3.11.html#pep-654-exception-groups-and-except). Exception groups are similar to task groups in that they give a new way to represent exceptions in `asyncio`. This now allows different coroutines to error in different ways and all the different exceptions will be collected into an [`ExceptionGroup`](https://docs.python.org/3/library/exceptions.html#ExceptionGroup), allowing you to handle each exception separately.

Sentry is currently evaluating how best to represent exception groups in Python and other languages. Come [join the conversation on GitHub](https://github.com/getsentry/sentry/issues/37716).

Let's look at an example:

```python
import asyncio

async def f1(x: int) -> None:
    await asyncio.sleep(x / 10)
    print(f'hi from {x}')

async def f2():
    raise ValueError(1)

async def f3():
    2 * 3 * (4 * None)

async def amain() -> int:
    # each of these 3 errors will happen in the background
    # and be collected into this TaskGroup
    async with asyncio.TaskGroup() as tg:
        for i in range(5):
            tg.create_task(f1(i))
        tg.create_task(f2())
        tg.create_task(f2())
        tg.create_task(f3())

    print('done')
    return 0

def main() -> int:
    return asyncio.run(amain())

if __name__ == '__main__':
    raise SystemExit(main())
```

With the introduction of exception groups, your output will still look a little wild, but it's much more logical than before.

This output shows our `ExceptionGroup` with our `TypeError` and our two `ValueError`s:

```output
hi from 0
+ Exception Group Traceback (most recent call last):
|   File "/Users/shanamatthews/src/git/sentry-blogs/exception_group.py", line 31, in <module>
|     raise SystemExit(main())
|                      ^^^^^^
|   File "/Users/shanamatthews/src/git/sentry-blogs/exception_group.py", line 28, in main
|     return asyncio.run(amain())
|            ^^^^^^^^^^^^^^^^^^^^
|   File "/Library/Frameworks/Python.framework/Versions/3.11/lib/python3.11/asyncio/runners.py", line 190, in run
|     return runner.run(main)
|            ^^^^^^^^^^^^^^^^
|   File "/Library/Frameworks/Python.framework/Versions/3.11/lib/python3.11/asyncio/runners.py", line 118, in run
|     return self._loop.run_until_complete(task)
|            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
|   File "/Library/Frameworks/Python.framework/Versions/3.11/lib/python3.11/asyncio/base_events.py", line 650, in run_until_complete
|     return future.result()
|            ^^^^^^^^^^^^^^^
|   File "/Users/shanamatthews/src/git/sentry-blogs/exception_group.py", line 17, in amain
|     async with asyncio.TaskGroup() as tg:
|   File "/Library/Frameworks/Python.framework/Versions/3.11/lib/python3.11/asyncio/taskgroups.py", line 135, in __aexit__
|     raise me from None
| ExceptionGroup: unhandled errors in a TaskGroup (3 sub-exceptions)
+-+---------------- 1 ----------------
| Traceback (most recent call last):
|   File "/Users/shanamatthews/src/git/sentry-blogs/exception_group.py", line 8, in f2
|     raise ValueError(1)
| ValueError: 1
+---------------- 2 ----------------
| Traceback (most recent call last):
|   File "/Users/shanamatthews/src/git/sentry-blogs/exception_group.py", line 8, in f2
|     raise ValueError(1)
| ValueError: 1
+---------------- 3 ----------------
| Traceback (most recent call last):
|   File "/Users/shanamatthews/src/git/sentry-blogs/exception_group.py", line 11, in f3
|     2 * 3 * (4 * None)
|              ~~^~~~~~
| TypeError: unsupported operand type(s) for *: 'int' and 'NoneType'
+------------------------------------
```

### Underline arrows

Another interesting thing to note in the exception output above are the underline arrows (e.g. `^^^^^^^^^^^^^^`). These arrows point to the exact expression that caused the error. This is new to all tracebacks and isn't specific to `asyncio`.

You can see in the final exception of the `ExceptionGroup` the `~~^~~~~~` points out the exact operator that caused a problem.

If we wanted to handle these errors we could do something like this:

```python
...

async def amain() -> int:
    try:
        async with asyncio.TaskGroup() as tg:
            for i in range(5):
                tg.create_task(f1(i))
            tg.create_task(f2())
            tg.create_task(f2())
            tg.create_task(f3())

    # we can catch the whole ExceptionGroup
    except ExceptionGroup as eg:
        print(f'got {eg}')

    print('done')
    return 0

...
```

And now our output would look like:

```output
hi from 0
got unhandled errors in a TaskGroup (3 sub-exceptions)
done
```

### `except*` syntax

Python 3.11 also includes new syntax for handling exception groups, which is the [`except*` syntax](https://docs.python.org/3/whatsnew/3.11.html#pep-654-exception-groups-and-except). This syntax allows you to collect exception groups of each of the types of exceptions that might be handled.

This would look like:

```python
...

async def amain() -> int:
    try:
        async with asyncio.TaskGroup() as tg:
            for i in range(5):
                tg.create_task(f1(i))
            tg.create_task(f2())
            tg.create_task(f2())
            tg.create_task(f3())

    # will collect all AssertionErrors into an ExceptionGroup
    except* TypeError as eg:
        print(f'got TE {eg}')

    # will collect all ValueErrors into an ExceptionGroup
    except* ValueError as eg:
        print(f'got VE {eg}')

    print('done')
    return 0

...
```

Now our output looks very sane:

```output
hi from 0
got TE unhandled errors in a TaskGroup (1 sub-exception)
got VE unhandled errors in a TaskGroup (2 sub-exceptions)
done
   ```

### Adding notes to exceptions

Python 3.11 also now allows you to [add notes to your exceptions](https://docs.python.org/3/whatsnew/3.11.html#pep-678-exceptions-can-be-enriched-with-notes) via the `add_note()` method.

This new feature could be useful in adding information to an exception as it bubbles up. Even if you don't get the information you'd need to change the type or re-raise the exception properly, you can still add extra context.

<!-- todo shana link to Sentry issue on notes? -->

Let's take our previous example code and add a new error type to demonstrate:

```python
...

async def f4():
    try:
        await f3()
    except TypeError as e:
        e.add_note('this failed while trying to blah')
        raise

async def amain() -> int:
   async with asyncio.TaskGroup() as tg:
       for i in range(5):
           tg.create_task(f1(i))
       tg.create_task(f2())
       tg.create_task(f2())
       tg.create_task(f4())

...
```

And here's a truncated version of the output where you can see the added note:

```output
...
+---------------- 3 ----------------
| Traceback (most recent call last):
|   File "/Users/shanamatthews/src/git/sentry-blogs/exception_group.py", line 15, in f4
|     await f3()
|   File "/Users/shanamatthews/src/git/sentry-blogs/exception_group.py", line 11, in f3
|     2 * 3 * (4 * None)
|              ~~^~~~~~
| TypeError: unsupported operand type(s) for *: 'int' and 'NoneType'
| this failed while trying to blah
+------------------------------------
```

## 5. Typing Improvements

Python 3.11 also comes with a lot of improvements to typing, so I'm splitting this into multiple sections as well.

### `Self` type

The [`Self`](https://docs.python.org/3/library/typing.html#typing.Self) type makes it easier to add types to certain categories of methods. One example is cloning. Previously, the type checker would believe that the output of `D.clone()` in the below example had type `C`:

```python
class C:
    def clone(self) -> C:
        return type(self)()

class D(C):
    pass

D.clone()  # type C, according to the typechecker
```

But now, we can use the `Self` type to correctly forward the type to the actual class:

```python
class C:
    def clone(self: Self) -> Self:
        return type(self)()

class D(C):
    pass

D.clone()  # type D, according to the typechecker
```

You can also use this with classmethods.

### Variadic Generics

[Variadic generics](https://docs.python.org/3/whatsnew/3.11.html#pep-646-variadic-generics) allow you to have variables that contain multiple types. This is especially important for tensor type objects (i.e. NumPy arrays, TensorFlow objects, Pandas, etc.) where you're representing arrays with multiple dimensions.

The 3.11 release added the new [`TypeVarTuple`](https://docs.python.org/3/library/typing.html#typing.TypeVarTuple), which makes it possible to have parameters with an arbitrary number of types, e.g. a variadic type variable, enabling variadic generics.

Here's some example code showing how `TypeVarTuple` can be used:

```python
from typing import TypeVarTuple

#  TypeVarTuple represents our multi-variable generic
Ts = TypeVarTuple('Ts')

# allows for multiple types
class Array(Generic[*Ts]):
    ...

# e.g. a 2d array with float data
x: Array[int, int, float]

# can also use in functions that transform them
def double(a: Array[*Ts]) -> Array[*Ts]:
    ...

# e.g. adding another dimension to our array
def add_dimention(a: Array[*Ts]) -> Array[int, *Ts]:
    ...

```

We're now also able to use the `*` (splat, unpack) operator inside tuples and inside of `*args`. This will make more sense in another example:

```python
from typing import TypeAlias

t: TypeAlias = tuple[int, int]

# use * to expand t
t2: TypeAlias = tuple[*t, float, str]  # tuple[int, int, float, str]

# use * to create a variable length tuple with fixed-length pre- or post-fix
# i.e. a string followed by a variable number of ints
t3: TypeAlias = tuple[str, *tuple[int, ...]]

# represents a function that takes a string as its first arg,
# then a variable number of ints
def f(*args: *t3):
    s, *ints = args # types are string, variable number of ints
```

### `LiteralString`

The [`LiteralString`](https://docs.python.org/3/whatsnew/3.11.html#pep-675-arbitrary-literal-string-type) annotation allows you to make a variable that has to be a string literal in your source code. One practical example of this is using the type checker to ban SQL injection, by forcing queries to come from literal strings, rather than formatted strings, i.e.:

```python
from typing import LiteralString

def execute_query(s: LiteralString) -> ...:
    ...

# allowed
execute_query('SELECT * FROM USERS')

# not allowed
users = '...'
execute_query('SELECT * FROM {}'.format(users))
```

### `Never`, `assert_never`, and `assert_type`

The [`Never`](https://docs.python.org/3/library/typing.html#typing.Never) type is a new alias for `NoReturn`. If you have a function that never completes, because it always raises an exception, loops forever, or some other reason, it can have a return type of `Never`.

```python
from typing import Never

def f1() -> Never:  # same as -> NoReturn
    ...
```

[`assert_never`](https://docs.python.org/3/library/typing.html#typing.assert_never) and [`assert_type`](https://docs.python.org/3/library/typing.html#typing.assert_type) are two new assert helpers that make the typechecker more useful.

`assert_never` uses the typechecker to confirm that code is not reachable. If the typechecker finds it is reachable, it emits an error. A call to `assert_never` won't pass type checking unless the inferred type of the argument passed in to `assert_never` is of type `Never`. This is useful for ensuring completeness in if statements and match case statements.

In the below example, the typechecker would give an error about the float type not being allowed in the `assert_never` function, and if we tried to pass a param of type float to `int_or_str` we'd get an exception at runtime.

```python
from typing import assert_never

def what_type(arg: int | str | float) -> None:
    match arg:
        case int():
            print("It's an int")
        case str():
            print("It's a str")
        case _ as unreachable:
            assert_never(unreachable) # typechecker error

what_type(1.0) # runtime exception
```

`assert_type()` lets you use the typechecker to ensure a variable has the type you intended. If your typechecker doesn't agree with you, you’ll get a typechecker error, but no errors at runtime.

```python
from typing import assert_never
from typing import assert_type

def what_type(arg: int | str) -> None:
    match arg:
        case int():
            print("It's an int")
        case str():
            print("It's a str")
            return
        case _ as unreachable:
            assert_never(unreachable)

    assert_type(arg, int) # you and your typechecker agree
    # assert_type(arg, str) # this would give a typechecker error
```

### `TypedDict` and `NamedTuple` can be generic

This is pretty straightforward. [`TypedDict`](https://docs.python.org/3/library/typing.html#typing.TypedDict) and [`NamedTuple`](https://docs.python.org/3/library/typing.html#typing.NamedTuple) can both now be generic. Here's example code for `TypedDict`:

```python
from typing import Generic

# using generic types inside our typed dictionary
class TypedDict(Generic[T]):
    x: T
```

## Wrap Up

Does this release include earth-shattering improvements that fundamentally change Python? No. But there are some noteworthy improvements that make Python faster, and easier to use. The seemingly minor improvements add up to make one of my favorite languages that much better.

There are many more features in Python 3.11 worth taking a look at. This piece was a collab with Anthony Sotille, [so check out this video from him](https://www.youtube.com/watch?v=w2rcZIG1Uxk) to learn even more.
