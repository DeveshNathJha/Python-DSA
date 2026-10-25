# Python and DSA: Complete Revision Notes

**How to use this file**

* Study the three notebooks first:
  1. `Python_Notes_1_Fundamentals.ipynb`
  2. `Python_Notes_2_Advanced_Python.ipynb`
  3. `Python_Notes_3_DSA_and_Interviews.ipynb`
* Then use this file to **revise everything in one place**. Every section here matches a Part in the notebooks.
* Each section has: key ideas, syntax tables, common mistakes, small code, and complexities.
* At the end of each big part there are **self-test questions**. Click "Answer" to check yourself.
* Notation: `O(n)` means the work grows in proportion to the input size `n`.
* Written for **Python 3.12+** (tested on Python 3.14). Newer features are marked, for example "(3.14+)".

---

## Table of contents

* **Part A: Python Fundamentals** (Notebook 1)
  A1 Getting started · A2 Variables and types · A3 Operators · A4 Input, output, conversion, f-strings ·
  A5 Conditions · A6 Loops · A7 Strings · A8 Lists and tuples · A9 Dictionaries and sets ·
  A10 References and copying · A11 Functions · A12 Errors and debugging · A13 Files and data formats ·
  A14 Modules and environments · Self-test A
* **Part B: Advanced Python** (Notebook 2)
  B1 OOP basics · B2 Inheritance and special methods · B3 Iterators and generators · B4 Decorators ·
  B5 Context managers · B6 Advanced features · B7 Standard library toolbox · B8 Concurrency ·
  B9 Testing, quality and security · Self-test B
* **Part C: DSA** (Notebook 3)
  C1 Interview method · C2 Complexity · C3 Math basics · C4 Arrays, strings, hashing · C5 Two pointers ·
  C6 Sliding window · C7 Recursion and backtracking · C8 Sorting · C9 Binary search · C10 Linked lists ·
  C11 Stacks and queues · C12 Heaps · C13 Trees and BST · C14 Tries · C15 Graphs · C16 Greedy and intervals ·
  C17 Dynamic programming · C18 Bit manipulation · Self-test C
* **Part D: Final Revision**
  D1 Pattern recognition sheet · D2 Python gotchas (predict the output) · D3 Debugging checklist ·
  D4 Last-day checklist

---

# Part A: Python Fundamentals

## A1. Getting started

* **Python** is a high-level, easy-to-read language. **Dynamically typed**: a variable can point to any type.
  **Strongly typed**: Python does not silently mix types (`"5" + 5` is a `TypeError`).
* **CPython** is the standard Python program (the one from python.org). It first compiles your code to
  **bytecode**, then the **Python Virtual Machine** runs it. So Python is "compiled to bytecode, then interpreted".
* Ways to run: interactive shell (`python`), script (`python app.py`), Jupyter notebook, IDE (VS Code, PyCharm).
* Use `python -m pip install x` so packages go into the same Python you run.
* Comments start with `#`. Python has **no multi-line comment syntax**; a `'''...'''` block is just a string.

**PEP 8 naming (the official style guide)**

| Kind | Style | Example |
|---|---|---|
| Variables, functions, modules | `snake_case` | `total_price`, `read_file()` |
| Classes, exceptions | `CapWords` | `BankAccount`, `ValidationError` |
| Constants | `UPPER_SNAKE_CASE` | `MAX_RETRIES` |
| Internal use | leading `_` | `_helper` |

* Identifiers: letters, digits, `_`; cannot start with a digit; case-sensitive; cannot be a keyword.
* Never use built-in names as variables (`list`, `dict`, `str`, `sum`, `max`, `id`, `input`).
  `sum = 0` then `sum([1, 2])` gives `TypeError: 'int' object is not callable`.

**How to think and write code**

```text
+-------------------+    +-------------------+    +------------------+
| 1. Understand the |--->| 2. Work 2-3       |--->| 3. Plan the steps|
|    problem        |    |    examples by    |    |    in plain words|
+-------------------+    |    hand           |    +--------+---------+
                         +-------------------+             |
                                                           v
+-------------------+    +-------------------+    +------------------+
| 6. Fix and test   |<---| 5. Test with      |<---| 4. Write small   |
|    again          |    |    normal + edge  |    |    pieces of code|
+-------------------+    |    cases          |    +------------------+
                         +-------------------+
```

---

## A2. Variables and data types

* A **variable is a name that points to an object**. `x = 5` makes the name `x` point to the object `5`.
  The **type belongs to the object**, not the name.
* `x, y = 1, 2` (multiple assignment), `x, y = y, x` (swap; the right side is built first),
  `a = b = 0` (two names, one object).

| Type | Example | Mutable? | Notes |
|---|---|---|---|
| `int` | `42`, `1_000_000`, `0xFF` | No | no size limit |
| `float` | `3.14`, `1e-3` | No | 64-bit, approximate |
| `complex` | `3+4j` | No | `.real`, `.imag` |
| `bool` | `True`, `False` | No | subclass of `int` (`True + True == 2`) |
| `str` | `"text"` | No | Unicode characters |
| `list` | `[1, 2]` | **Yes** | ordered |
| `tuple` | `(1, 2)` | No | ordered |
| `dict` | `{"a": 1}` | **Yes** | keeps insertion order (3.7+) |
| `set` | `{1, 2}` | **Yes** | unique, unordered |
| `NoneType` | `None` | No | "no value"; test with `is None` |

* `type(x)` gives the exact type. `isinstance(x, int)` also accepts subclasses; prefer it.
  Note: `isinstance(True, int)` is `True`.
* **Floats are approximate**: `0.1 + 0.2 == 0.3` is `False`. Use `math.isclose(a, b)` to compare,
  and `decimal.Decimal("0.1")` (or integer cents) for money.
* `round()` uses **round half to even** (banker's rounding): `round(2.5) == 2`, `round(3.5) == 4`.

```python
import math
from decimal import Decimal

print(0.1 + 0.2 == 0.3)                      # False
print(math.isclose(0.1 + 0.2, 0.3))          # True
print(Decimal("0.1") + Decimal("0.2"))       # 0.3
print(round(2.5), round(3.5))                # 2 4
print(2 ** 100)                              # ints never overflow
```

---

## A3. Operators

| Group | Operators |
|---|---|
| Arithmetic | `+ - * / // % **` |
| Comparison | `== != < <= > >=` (can be chained: `1 < x < 10`) |
| Logical | `and or not` (short-circuit; return one of the operands) |
| Identity / membership | `is`, `is not`, `in`, `not in` |
| Bitwise | `&` `\|` `^` `~` `<<` `>>` |
| Assignment | `= += -= *= /= //= %= **=`, walrus `:=` (assign inside an expression) |

**Division and rounding (very common in interviews)**

| Expression | Result | Meaning |
|---|---|---|
| `7 / 2` | `3.5` | true division, **always a float** |
| `7 // 2` | `3` | floor division (rounds **down**) |
| `-7 // 2` | `-4` | floor goes toward minus infinity, not toward zero |
| `-7 % 3` | `2` | the result has the sign of the divisor |
| `int(-7 / 2)` | `-3` | truncates toward zero |
| `divmod(17, 5)` | `(3, 2)` | quotient and remainder together |

* `math.floor(x)`: always moves **left** on the number line (`2.9 -> 2`, `-2.1 -> -3`).
* `math.ceil(x)`: always moves **right** (`2.1 -> 3`, `-2.9 -> -2`).
* `math.trunc(x)` and `int(x)`: cut off the decimal part, i.e. move **toward zero** (`-2.9 -> -2`).
* Problems like "Divide Two Integers" or "String to Integer (atoi)" need **rounding toward zero**:
  use `int(a / b)` (or `math.trunc`), not `a // b`, and not `round()`.
* The rule that always holds: `a == (a // b) * b + a % b`.

**Precedence (high to low)**: `()` -> `**` -> unary `-x` -> `* / // %` -> `+ -` -> shifts -> `&` -> `^` -> `|`
-> comparisons, `in`, `is` -> `not` -> `and` -> `or` -> `if-else` -> `lambda` -> `:=`.

* `-2 ** 2 == -4` (power first). `2 ** 3 ** 2 == 512` (`**` is right-to-left).
* `x == 1 or 2` is always truthy (it means `(x == 1) or 2`). Write `x in (1, 2)`.
* `and`/`or` return an operand: `0 or "default"` gives `"default"`; `[] and 5` gives `[]`.
* `==` compares values, `is` compares identity (same object). Use `is` only for `None`, `True`, `False`.

---

## A4. Input, output, type conversion, f-strings

* `print(*items, sep=" ", end="\n")`. `print(*[1, 2, 3])` prints `1 2 3`.
* `input()` **always returns a string**. Convert it: `age = int(input("Age: "))`.
* Conversion rules:
  * `int("42") == 42`, `int(3.99) == 3` (truncates), `int("3.5")` is a `ValueError`, `int("ff", 16) == 255`.
  * `bool(x)` is `False` only for empty or zero values. `bool("False")` is `True` (non-empty string).
  * Only numbers convert automatically (`1 + 2.0 == 3.0`). Everything else needs explicit conversion.
* Escape sequences: `\n` newline, `\t` tab, `\\` backslash, `\'` quote. Raw strings: `r"C:\new"`.

**f-string format spec**: `f"{value:[fill][align][sign][width][,][.precision][type]}"`

| Goal | Code | Result |
|---|---|---|
| 2 decimals | `f"{3.14159:.2f}"` | `3.14` |
| width + align | `f"{'hi':>6}"`, `f"{'hi':<6}"`, `f"{'hi':^6}"` | `'    hi'`, `'hi    '`, `'  hi  '` |
| zero padding | `f"{42:05d}"` | `00042` |
| thousands | `f"{1234567:,}"` | `1,234,567` |
| percent | `f"{0.256:.1%}"` | `25.6%` |
| binary / hex | `f"{5:b}"`, `f"{255:#x}"` | `101`, `0xff` |
| debug form | `f"{x = }"` | `x = 7` |

---

## A5. Conditions

```text
        +-------------+  True   +-----------+
        | condition 1 |-------->| block 1   |----+
        +------+------+         +-----------+    |
               | False                           |
               v                                 |
        +-------------+  True   +-----------+    |
        | condition 2 |-------->| block 2   |----+
        +------+------+         +-----------+    |
               | False                           |
               v                                 v
        +-------------+                   +-------------+
        | else block  |------------------>| next line   |
        +-------------+                   +-------------+
```

* The **first** true branch runs; the rest are skipped. Order matters (check `>= 90` before `>= 80`).
* **Falsy values**: `None`, `False`, `0`, `0.0`, `""`, `[]`, `()`, `{}`, `set()`, `range(0)`. Everything else is truthy.
* `if not items:` tests emptiness. When `0` is a valid value, test `if value is None:` instead.
* Conditional expression: `label = "adult" if age >= 18 else "minor"`.
* **match/case** (3.10+) matches structure: literals, `|`, sequences `[x, y]`, mappings `{"k": v}`,
  classes `Point(x=0)`, guards `if`, wildcard `_`. A bare name in a pattern **captures**, it does not compare.

---

## A6. Loops

* `for x in iterable:` runs once per item. `while condition:` repeats while the condition is true.
* `range(start, stop, step)`: **stop is excluded**. It is lazy (no list is built).
* `break` leaves the loop. `continue` skips to the next item.
* The loop `else` runs **only if the loop did not hit `break`** (read it as "no break").

```text
   +-------> take next item? ---- no more items ----> run else block ---> done
   |               |
   |              yes
   |               v
   |         run loop body
   |          |         |
   |   continue/end    break ---------------------------------------------> done
   +----------+                                   (else block is skipped)
```

```python
def is_prime(n):
    if n < 2:                                # 0 and 1 are not prime
        return False
    for d in range(2, int(n ** 0.5) + 1):   # only check up to sqrt(n)
        if n % d == 0:
            return False
    return True

def describe(n):
    if n < 2:
        return "not prime"
    for d in range(2, int(n ** 0.5) + 1):
        if n % d == 0:
            return "not prime"
    else:                                    # no divisor found
        return "prime"

print([p for p in range(20) if is_prime(p)])  # [2, 3, 5, 7, 11, 13, 17, 19]
print(describe(1), describe(13))               # not prime prime
```

**Helpers**: `enumerate(seq, start=0)` (index + value), `zip(a, b, strict=True)` (parallel; 3.10+ strict
raises if lengths differ), `reversed(seq)`, `sorted(seq, key=..., reverse=...)`.

**Common mistakes**

* Changing a list while looping over it skips items. Build a new list: `[x for x in nums if x % 2]`.
* Forgetting to update the variable in a `while` loop gives an infinite loop.
* The loop variable still exists after the loop (`for i in range(3)` leaves `i == 2`).

---

## A7. Strings

* Strings are **immutable**: every method returns a **new** string. `s.upper()` alone changes nothing; write `s = s.upper()`.
* Slicing `s[start:stop:step]`, stop excluded. `s[::-1]` reverses. Slicing never raises an `IndexError`; indexing does.

```text
 P   y   t   h   o   n
 0   1   2   3   4   5     positive index
-6  -5  -4  -3  -2  -1     negative index
```

| Task | Method |
|---|---|
| clean | `strip()`, `lstrip()`, `rstrip()`, `removeprefix()`, `removesuffix()` |
| case | `lower()`, `upper()`, `title()`, `capitalize()`, `casefold()` (best for comparing) |
| search | `find()` (returns -1), `index()` (raises ValueError), `count()`, `in`, `startswith()`, `endswith()` |
| split / join | `split(sep=None, maxsplit=-1)`, `rsplit()`, `splitlines()`, `partition()`, `sep.join(items)` |
| replace | `replace(old, new, count)`, `translate(str.maketrans(...))` |
| checks | `isdigit()`, `isalpha()`, `isalnum()`, `isspace()`, `islower()`, `isupper()` (all `False` for `""`) |
| pad | `zfill()`, `ljust()`, `rjust()`, `center()` |

* `split()` with no argument splits on any run of whitespace and drops empty strings; `split(" ")` keeps empty strings.
* Build big strings with `"".join(parts)` (linear time), not `+=` in a loop (can be quadratic).
* `ord("a") == 97`, `chr(97) == "a"`. Letter index: `ord(ch) - ord("a")`.
* Text vs bytes: `"café".encode("utf-8")` gives 5 bytes; `bytes.decode("utf-8")` gives text back.
* String comparison is by code point, so `"Z" < "a"`. Use `key=str.casefold` for human ordering.

| Operation | Cost |
|---|---|
| `len(s)`, `s[i]` | O(1) |
| `s[a:b]`, `s + t`, `x in s`, `s == t` | O(n) |
| `"".join(parts)` | O(total length) |

---

## A8. Lists and tuples

| Operation | Example | Time |
|---|---|---|
| access / update | `a[i]`, `a[i] = x` | O(1) |
| append, pop from end | `a.append(x)`, `a.pop()` | O(1) amortised |
| insert / delete in the middle | `a.insert(i, x)`, `a.pop(i)`, `del a[i]` | O(n) |
| search | `x in a`, `a.index(x)`, `a.count(x)` | O(n) |
| slice / copy | `a[i:j]`, `a.copy()` | O(k) |
| sort | `a.sort()`, `sorted(a)` | O(n log n), stable |
| extend | `a.extend(b)` | O(len(b)) |

* Methods that change the list in place return **None**: `append`, `extend`, `insert`, `remove`, `sort`, `reverse`, `clear`.
  `nums = nums.sort()` destroys your list. Use `sorted(nums)` to get a new list.
* `[[0] * 3] * 3` creates **three references to the same row**. Use `[[0] * 3 for _ in range(3)]`.
* Slicing tricks: `a[::-1]` reverse, `a[-k:]` last k, `a[::2]` every second item, `a[:]` shallow copy.
* **Comprehensions**: `[x * x for x in nums if x % 2 == 0]`; with if/else the condition goes before `for`:
  `["even" if x % 2 == 0 else "odd" for x in nums]`. Nested: `[v for row in grid for v in row]`.
* **Tuples** are immutable and hashable (if their items are), so they can be dict keys: `grid[(r, c)]`.
  One-item tuple needs a comma: `(5,)`. Immutability is shallow: `([1], 2)[0].append(3)` works.
* Unpacking: `first, *rest = [1, 2, 3]`, `a, (b, c) = 1, (2, 3)`, `print(*items)`, `f(*args, **kwargs)`.

---

## A9. Dictionaries and sets

* A dict is a **hash table**: lookup, insert and delete are **O(1) on average**. Keys must be **hashable**
  (immutable: `int`, `str`, `tuple` of hashables, `frozenset`). Since 3.7 dicts keep insertion order.

| Need | Code |
|---|---|
| safe read | `d.get(key, default)` |
| read or insert default | `d.setdefault(key, []).append(x)` |
| remove | `d.pop(key, default)`, `del d[key]`, `d.popitem()` (last inserted) |
| loop | `for k, v in d.items():` |
| merge (3.9+) | `d1 \| d2` (right side wins), `d1.update(d2)` |
| build | `dict(zip(keys, values))`, `dict.fromkeys(keys, 0)`, `{k: v for k, v in pairs}` |
| filter | `{k: v for k, v in d.items() if v > 1}` |

* Counting: `counts[x] = counts.get(x, 0) + 1`, or `collections.Counter(items)`.
* Grouping: `groups.setdefault(key, []).append(item)`, or `collections.defaultdict(list)`.
* Do not add or remove keys while looping over a dict (`RuntimeError`). Loop over `list(d)` instead.
* **Sets**: unique items, O(1) average `in`. `{}` is an **empty dict**; use `set()`.
  Operations: `a | b` union, `a & b` intersection, `a - b` difference, `a ^ b` symmetric difference.
* Remove duplicates: `set(items)` (loses order) or `list(dict.fromkeys(items))` (keeps first-seen order).
* Sorting by a key: `sorted(people, key=lambda p: (-p.age, p.name))` (age descending, name ascending).
  Sort is **stable**: equal keys keep their original order.

**Choosing a data structure**

| Need | Use | Why |
|---|---|---|
| ordered items, index access | `list` | O(1) index |
| "have I seen this?" | `set` | O(1) membership |
| key -> value, counting, grouping | `dict` / `Counter` / `defaultdict` | O(1) lookup |
| queue (FIFO), both ends | `collections.deque` | O(1) at both ends |
| always get the smallest/largest | `heapq` | O(log n) push/pop |
| keep a sorted list and search it | `bisect` | O(log n) search |
| fixed record, dict key | `tuple` | immutable, hashable |

---

## A10. References, mutability and copying

* Assignment never copies: `b = a` makes two names for **one** object. Changing it through `b` is visible through `a`.
* **Mutable**: `list`, `dict`, `set`, most objects. **Immutable**: `int`, `float`, `str`, `tuple`, `frozenset`, `None`.
* **Rebinding** (`x = x + [1]`) creates a new object. **Mutation** (`x.append(1)`, `x += [1]` for lists) changes the shared object.
* Function arguments are passed **by object reference**: mutating a parameter affects the caller;
  rebinding the parameter does not.

| Copy | Code | Inner objects |
|---|---|---|
| no copy | `b = a` | shared (same object) |
| shallow | `a.copy()`, `a[:]`, `list(a)`, `dict(d)` | **shared** |
| deep | `copy.deepcopy(a)` | copied |

* 2D grid copy: `[row[:] for row in grid]` or `copy.deepcopy(grid)`; `grid.copy()` still shares rows.
* Backtracking: store `result.append(path[:])`, not `result.append(path)`.
* Small integers and some strings are cached by CPython, so `is` may look like `==`. Never rely on it.

```python
import copy

a = [[1, 2], [3, 4]]
shallow = a.copy()
deep = copy.deepcopy(a)
a[0][0] = 99
print(shallow[0][0], deep[0][0])   # 99 1
```

---

## A11. Functions

* `return` gives a value back; `print` only displays. A function without `return` returns `None`.
* Parameter order: `def f(pos_only, /, normal, *args, kw_only, **kwargs)`.
  `*args` collects extra positional arguments into a tuple; `**kwargs` collects extra keyword arguments into a dict.
* **Mutable default trap**: defaults are created **once**, when `def` runs.

```python
def add_item(item, bucket=None):    # correct pattern
    if bucket is None:
        bucket = []
    bucket.append(item)
    return bucket

print(add_item(1), add_item(2))     # [1] [2]
```

* **Scope (LEGB)**: Python looks for a name in **L**ocal -> **E**nclosing -> **G**lobal -> **B**uilt-in.
  Assigning to a name inside a function makes it local, so reading it first raises `UnboundLocalError`.
  Use `global x` (module variable) or `nonlocal x` (enclosing function variable) to rebind outer names.
* **Closure**: an inner function that remembers variables of the outer function.
  **Late binding**: `[lambda: i for i in range(3)]` all return 2. Fix: `lambda i=i: i`.
* `lambda x: x * 2` is a one-expression function; good for `key=` arguments.
* `map(f, items)`, `filter(pred, items)` return lazy iterators. Comprehensions are usually clearer.
* `functools.reduce(lambda acc, x: acc + x, items, 0)`. Prefer `sum`, `max`, `math.prod` when they fit.
* `any([])` is `False`, `all([])` is `True`. `max(items, key=len)`, `min(d, key=d.get)`, `max([], default=0)`.
* **Recursion**: needs a base case; default depth limit about 1000 (`sys.getrecursionlimit()`);
  no tail-call optimisation. Repeated subproblems: memoise with a dict or `@functools.cache`.
* Type hints (`def f(x: int) -> str:`) are **not checked at run time**; tools like mypy check them.

---

## A12. Errors, exceptions and debugging

| Kind | When found | Example |
|---|---|---|
| Syntax error | before running | missing `:` or bracket |
| Runtime error (exception) | while running | `1 / 0`, `int("x")`, `d["missing"]` |
| Logic error | never by Python | wrong formula, `<` instead of `<=` |

```text
try:      code that might fail
except:   runs only if a matching exception happened (first match wins, put specific ones first)
else:     runs only if NO exception happened
finally:  ALWAYS runs (cleanup), even after return or an exception
```

```text
BaseException
 +-- KeyboardInterrupt, SystemExit, GeneratorExit   (do not catch casually)
 +-- Exception
      +-- ArithmeticError: ZeroDivisionError, OverflowError
      +-- LookupError: IndexError, KeyError
      +-- ValueError, TypeError, AttributeError, NameError (UnboundLocalError)
      +-- OSError: FileNotFoundError, PermissionError, TimeoutError
      +-- RuntimeError: RecursionError, NotImplementedError
      +-- ImportError: ModuleNotFoundError
      +-- StopIteration, AssertionError
```

```python
class InsufficientFundsError(Exception):       # a custom exception is a class
    pass

def parse_age(text):
    try:
        age = int(text)
    except ValueError as e:                     # catch the specific error
        raise ValueError(f"age must be a number, got {text!r}") from e
    if age < 0:
        raise ValueError("age must be >= 0")
    return age

for raw in ["25", "abc", "-3"]:
    try:
        print(parse_age(raw))
    except ValueError as e:
        print("Error:", e)
```

* Do not use bare `except:` (it also catches Ctrl-C). Never `except: pass` (hides bugs).
* `raise` alone re-raises the current exception; `raise New(...) from e` keeps the original cause.
* `assert` is for programmer checks only; it is removed with `python -O`. Validate user input with `if ... raise`.
* **EAFP** (try, then handle the error) is the Pythonic style: `try: v = d[k] except KeyError: ...`.

**Common error messages**

| Message | Usual cause | Fix |
|---|---|---|
| `NameError: name 'x' is not defined` | typo, or used before assignment | check spelling and order |
| `TypeError: can only concatenate str (not "int") to str` | `"a" + 5` | `str(5)` or an f-string |
| `TypeError: 'NoneType' object is not subscriptable` | a function returned `None` (e.g. `x = lst.sort()`) | use the return value correctly |
| `IndexError: list index out of range` | off-by-one, empty list | check bounds, `range(len(a))` |
| `KeyError: 'k'` | missing dict key | `d.get(k)`, `in` check |
| `AttributeError: 'list' object has no attribute 'add'` | wrong method for the type | check the type |
| `UnboundLocalError` | assigning to a global name inside a function | pass it in / return it, or `global` |
| `RecursionError` | missing or wrong base case, too deep | fix base case, use iteration |
| `ValueError: invalid literal for int()` | bad text conversion | validate with `try/except` |
| `IndentationError` | mixed tabs/spaces or wrong indent | use 4 spaces |

**Debugging process**

```text
+--------------------+    +-----------------------+    +--------------------+
| Reproduce the bug  |--->| Read the traceback    |--->| Find the exact line|
| with a small input |    | from the BOTTOM up    |    | and the bad value  |
+--------------------+    +-----------------------+    +---------+----------+
                                                                 |
+--------------------+    +-----------------------+    +---------v----------+
| Add a test so it   |<---| Fix and re-run all    |<---| Inspect values:    |
| never comes back   |    | tests                 |    | print(f"{x=}") or  |
+--------------------+    +-----------------------+    | the debugger       |
                                                       +--------------------+
```

* Print debugging: `print(f"{i=} {total=}")`. Remove or turn into logging afterwards.
* Debugger: put `breakpoint()` in the code (starts `pdb`), or click a breakpoint in VS Code / Jupyter.

| pdb command | Meaning |
|---|---|
| `n` | next line (step over) |
| `s` | step into a function |
| `c` | continue to the next breakpoint |
| `p expr` / `pp expr` | print / pretty-print a value |
| `l` / `ll` | list source around the current line / whole function |
| `w`, `u`, `d` | where (call stack), move up / down the stack |
| `b 25` | set a breakpoint at line 25 |
| `q` | quit |

* Other techniques: shrink the input until the bug remains, explain the code line by line
  ("rubber duck"), comment out half of the code to find the broken half (bisecting), use `logging`.

---

## A13. Files and data formats

* Always: `with open(path, "r", encoding="utf-8") as f:` (the file is closed automatically).
* Modes: `"r"` read, `"w"` write (**erases**), `"a"` append, `"x"` create only, `"b"` binary, `"+"` read and write.
* Read big files line by line: `for line in f:` (constant memory). `f.read()` loads everything.
* `pathlib.Path`: `Path("data") / "file.txt"`, `.exists()`, `.read_text()`, `.write_text()`, `.glob("*.csv")`,
  `.rglob(...)`, `.mkdir(parents=True, exist_ok=True)`, `.name`, `.stem`, `.suffix`, `.parent`.
* `shutil.copy`, `shutil.move`, `shutil.rmtree` (careful); `tempfile.TemporaryDirectory()` for scratch work.
* **CSV**: open with `newline=""`; `csv.DictReader` / `csv.DictWriter`; all values come back as strings.
* **JSON**: `json.dumps` / `json.loads` (strings), `json.dump` / `json.load` (files). Tuples become lists,
  dict keys become strings; `set` and `datetime` need `default=`.
* **pickle** can run code when loading: never unpickle untrusted data.

---

## A14. Modules, packages and environments

* A **module** is a `.py` file; a **package** is a folder of modules (normally with `__init__.py`).
* A module runs **once** on the first import, then it is cached in `sys.modules`.
* `if __name__ == "__main__":` runs code only when the file is executed directly, not when imported.
* Import search order: `sys.modules` -> built-in modules -> folders in `sys.path` (script folder first).
  Naming your file `random.py` or `json.py` **shadows** the standard module.
* Circular import fix: move shared code to a third module, or import the module (not the name) and use it later.
* Virtual environment per project:

```text
python -m venv .venv
.venv\Scripts\activate            (Windows)     source .venv/bin/activate   (macOS/Linux)
python -m pip install requests
python -m pip freeze > requirements.txt
python -m pip install -r requirements.txt
```

* Project settings live in `pyproject.toml`. Modern tools: `uv` (fast installer and project manager), `ruff` (linter/formatter), `mypy` (types), `pytest` (tests).

---

## Self-test A

1. What does `print(-7 // 2, -7 % 2, int(-7 / 2))` print?
   <details><summary>Answer</summary>

   `-4 1 -3`. `//` floors toward minus infinity; `%` takes the divisor's sign; `int()` truncates toward zero.
   </details>

2. What does this print?

   ```python
   def f(x, items=[]):
       items.append(x)
       return items

   print(f(1), f(2))
   ```

   <details><summary>Answer</summary>

   `[1, 2] [1, 2]`. The default list is created once and shared; both calls return the same list.
   </details>

3. Why is `nums = nums.sort()` a bug?
   <details><summary>Answer</summary>

   `list.sort()` sorts in place and returns `None`, so `nums` becomes `None`. Use `nums.sort()` or `nums = sorted(nums)`.
   </details>

4. What does `grid = [[0] * 2] * 2; grid[0][0] = 1; print(grid)` print?
   <details><summary>Answer</summary>

   `[[1, 0], [1, 0]]`. Both rows are the same list object. Build rows with a comprehension.
   </details>

5. Difference between `is` and `==`?
   <details><summary>Answer</summary>

   `==` compares values; `is` checks that both names point to the same object. Use `is` for `None`.
   </details>

6. What does this print?

   ```python
   for n in [3, 5, 7]:
       if n % 2 == 0:
           break
   else:
       print("no even number")
   ```

   <details><summary>Answer</summary>

   `no even number`. The loop finished without `break`, so the `else` block ran.
   </details>

7. Why does this raise `UnboundLocalError`?

   ```python
   count = 0

   def increment():
       count += 1
   ```

   <details><summary>Answer</summary>

   Assigning to `count` makes it local to the function, but it is read before it has a value. Pass the value in and
   return the new value, or (less ideal) declare `global count`.
   </details>

8. Name two ways to remove duplicates from a list, one that keeps the order.
   <details><summary>Answer</summary>

   `list(set(items))` (order lost) and `list(dict.fromkeys(items))` (keeps first-seen order).
   </details>

---
# Part B: Advanced Python

## B1. OOP basics: classes and objects

* A **class** is a blueprint; an **object** (instance) is a thing built from it.
* `__new__` creates the object, `__init__` fills in its data. Python calls both for you: `acct = Account("Asha")`.
* `self` is the instance the method was called on: `acct.deposit(50)` means `Account.deposit(acct, 50)`.

```text
+--------------------------------------+
| class Employee                       |
|   company = "XYZ"   (class attribute,|
|                      shared)         |
+-------------------+------------------+
        ^ lookup falls back to the class
        |                       |
+-------+---------+     +-------+---------+
| e1.__dict__     |     | e2.__dict__     |
| name = "Ram"    |     | name = "Prerna" |
+-----------------+     +-----------------+
```

* Attribute lookup: instance `__dict__` -> class -> parent classes (MRO).
* `e1.company = "ABC"` creates a **new instance attribute** that hides the class one (only for `e1`).
* A **mutable class attribute** (e.g. `members = []`) is shared by all instances. Create it in `__init__` instead.

| Method type | Decorator | First parameter | Use for |
|---|---|---|---|
| instance method | none | `self` | normal behaviour using object data |
| class method | `@classmethod` | `cls` | alternative constructors (`from_string`), class-wide data |
| static method | `@staticmethod` | none | helper that belongs to the class but needs no object or class data |

* `_name` = "internal, please do not touch" (convention). `__name` = name mangling to `_Class__name`
  (avoids clashes in subclasses). Neither is real privacy.
* **Property**: a method that looks like an attribute. The getter **returns** a value; the setter validates.

```python
class Temperature:
    def __init__(self, celsius):
        self.celsius = celsius            # goes through the setter

    @property
    def celsius(self):
        return self._celsius

    @celsius.setter
    def celsius(self, value):
        if value < -273.15:
            raise ValueError("below absolute zero")
        self._celsius = value

    @property
    def fahrenheit(self):                 # read-only computed attribute
        return self._celsius * 9 / 5 + 32

    @classmethod
    def from_fahrenheit(cls, f):          # alternative constructor
        return cls((f - 32) * 5 / 9)

    def __repr__(self):
        return f"Temperature({self._celsius!r})"

t = Temperature.from_fahrenheit(212)
print(t, t.fahrenheit)                    # Temperature(100.0) 212.0
```

* `__str__` = readable text for users (`print`); `__repr__` = unambiguous text for developers (shell, lists).
  `print` falls back to `__repr__` if there is no `__str__`.

---

## B2. Inheritance, polymorphism and special methods

* **Inheritance** ("is-a"): `class Manager(Employee)`. Override methods; call the parent with `super().__init__(...)`.
* Types: single, multilevel (A -> B -> C), hierarchical (one parent, many children), multiple (`class C(A, B)`).
* **MRO** (method resolution order): the order Python searches classes. See it with `C.__mro__`.
  `super()` means "the next class in the MRO", not always "my parent".

```text
        A            class D(B, C)
       / \           D.__mro__ = D -> B -> C -> A -> object
      B   C          each class appears once; children before parents
       \ /
        D
```

* **Composition** ("has-a"): a `Car` has an `Engine`. Prefer composition over deep inheritance.
* **Polymorphism / duck typing**: any object with the right method works ("if it quacks like a duck").
* **Abstract base class**: `from abc import ABC, abstractmethod`; a subclass that does not implement every
  abstract method cannot be created (`TypeError`).

**Special ("dunder") methods**

| Syntax | Method |
|---|---|
| `str(x)`, `repr(x)` | `__str__`, `__repr__` |
| `len(x)`, `x[i]`, `x[i] = v`, `v in x` | `__len__`, `__getitem__`, `__setitem__`, `__contains__` |
| `for v in x` | `__iter__` (and `__next__` on the iterator) |
| `a + b`, `a * b`, `b + a` | `__add__`, `__mul__`, `__radd__` |
| `a == b`, `a < b`, `hash(a)` | `__eq__`, `__lt__`, `__hash__` |
| `bool(x)`, `x()` | `__bool__`, `__call__` |
| `with x:` | `__enter__`, `__exit__` |

* Return `NotImplemented` (do not raise) from operators when the other type is not supported.
* If you define `__eq__`, also define `__hash__` (or the objects become unhashable). Equal objects must have equal hashes.
* `@functools.total_ordering` builds `<=, >, >=` from `__eq__` and `__lt__`.

**Dataclasses** remove boilerplate for data-holding classes:

```python
from dataclasses import dataclass, field

@dataclass(order=True, frozen=True)
class Point:
    x: int
    y: int

@dataclass
class Order:
    order_id: int
    items: list = field(default_factory=list)   # never use a plain [] default

    def __post_init__(self):
        if self.order_id <= 0:
            raise ValueError("order_id must be positive")

print(Point(1, 2) < Point(1, 3), {Point(0, 0): "origin"})   # True {Point(x=0, y=0): 'origin'}
print(Order(7))                                              # Order(order_id=7, items=[])
```

* Options: `frozen=True` (immutable, hashable), `order=True` (comparisons), `slots=True` (less memory), `kw_only=True`.
* `__slots__ = ("a", "b")` removes the per-object `__dict__`: less memory, no new attributes.
* `Enum` for named constants: `class Color(Enum): RED = 1`. `IntEnum`, `StrEnum` (3.11+), `Flag`, `auto()`.
* Design principles: one class = one responsibility; depend on behaviour (interfaces), not concrete classes;
  keep it simple; do not repeat yourself.

---

## B3. Iterators and generators

* **Iterable**: can be looped over (`__iter__`): list, str, dict, set, range, file.
* **Iterator**: gives the next value with `next()` (`__next__`) and remembers its position. **One-shot**: once used up it stays empty.
* A `for` loop does: `it = iter(obj)`, then calls `next(it)` until `StopIteration`.
* **Generator function**: any function with `yield`. Calling it returns a generator; each `next()` runs until the next `yield` and **pauses** there.

```python
def countdown(n):
    while n > 0:
        yield n          # pause here and hand out n
        n -= 1

gen = countdown(3)
print(next(gen), list(gen), list(gen))   # 3 [2, 1] []
squares = (x * x for x in range(5))      # generator expression (lazy)
print(sum(squares))                      # 30
```

* Generators use constant memory: perfect for big files, streams, infinite sequences and pipelines.
* `yield from other` hands out everything from another iterable.
* Do not use a generator when you need `len()`, indexing, or several passes over the data.

---

## B4. Closures and decorators

* A **decorator** takes a function and returns a new function. `@timer` above `def f` means `f = timer(f)`.
* Decorator code runs at **definition time**; the wrapper runs at **call time**.

```python
import functools
import time

def timer(func):
    @functools.wraps(func)                 # keep the name and docstring
    def wrapper(*args, **kwargs):          # accept any arguments
        start = time.perf_counter()
        result = func(*args, **kwargs)
        elapsed = time.perf_counter() - start
        print(f"{func.__name__} finished ({elapsed >= 0})")
        return result                      # do not forget to return
    return wrapper

def retry(times):                          # decorator WITH arguments: one more layer
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(1, times + 1):
                try:
                    return func(*args, **kwargs)
                except ConnectionError:
                    if attempt == times:
                        raise
        return wrapper
    return decorator

calls = {"n": 0}

@timer
@retry(times=3)                            # stacked: applied bottom-up
def fetch():
    calls["n"] += 1
    if calls["n"] < 3:
        raise ConnectionError("try again")
    return "data"

print(fetch(), calls["n"])                 # fetch finished (True) / data 3
```

* Built-in decorators to know: `@functools.cache` / `@lru_cache(maxsize=...)` (memoisation), `@property`,
  `@classmethod`, `@staticmethod`, `@dataclass`, `@contextmanager`.

---

## B5. Context managers

* `with obj as x:` calls `obj.__enter__()` (its return value becomes `x`) and **always** calls `__exit__` at the end,
  even on errors. If `__exit__` returns `True`, the exception is suppressed.
* Easiest way to write one: `@contextlib.contextmanager` with `try: yield ... finally: cleanup`.
* Useful tools: `contextlib.suppress(FileNotFoundError)`, `redirect_stdout`, `ExitStack`, `closing`, `nullcontext`.
* Uses: files, locks, database transactions, timers, temporary settings.

---

## B6. Advanced language features

* Everything is an object (functions and classes too). Introspection: `type`, `dir`, `vars`, `getattr`,
  `hasattr`, `setattr`, `callable`, `inspect.signature`.
* `__getattribute__` runs on **every** attribute access; `__getattr__` runs **only when normal lookup fails**.
* **Descriptors** (`__get__`, `__set__`) power `property`, methods, `classmethod`, `staticmethod`.
* Class creation hooks, simplest first: class decorator -> `__init_subclass__` -> metaclass (rarely needed).
* Typing: `list[int]`, `dict[str, int]`, `int | None`, `Callable[[int], str]`, `TypeVar`, `Protocol`
  (structural typing), `TypedDict`, `Literal`, `Final`. Python 3.12 generic syntax: `def first[T](xs: list[T]) -> T:`.
* Memory (CPython): **reference counting** frees objects at once when no one refers to them; a
  **cycle collector** (`gc`) frees reference cycles. `weakref` refers to an object without keeping it alive.

---

## B7. Standard library toolbox

**collections**

```python
from collections import Counter, defaultdict, deque, namedtuple, OrderedDict

c = Counter("abracadabra")
print(c.most_common(2), c["z"])          # [('a', 5), ('b', 2)] 0

groups = defaultdict(list)               # missing keys start as []
for word in ["apple", "avocado", "banana"]:
    groups[word[0]].append(word)
print(dict(groups))                      # {'a': ['apple', 'avocado'], 'b': ['banana']}

q = deque([1, 2, 3])
q.appendleft(0); q.append(4)
print(q.popleft(), q.pop(), q)           # 0 4 deque([1, 2, 3])
recent = deque(maxlen=2)                 # keeps only the last 2 items
recent.extend([1, 2, 3])
print(recent)                            # deque([2, 3], maxlen=2)

Pt = namedtuple("Pt", "x y")
print(Pt(1, 2).x)                        # 1

lru = OrderedDict()
lru["a"] = 1; lru["b"] = 2
lru.move_to_end("a")                     # mark "a" as recently used
print(lru.popitem(last=False))           # ('b', 2)  oldest removed
```

* Reading a missing key in a `defaultdict` **creates** it. Use `in` or `.get()` just to check.

**deque vs list**

| Operation | list | deque |
|---|---|---|
| append / pop at the right | O(1) | O(1) |
| insert / pop at the left (`pop(0)` vs `popleft()`) | O(n), shifts every item | O(1) |
| index in the middle | O(1) | O(n) |
| best for | random index access | queues, BFS, sliding windows |

**heapq (min-heap)**

```python
import heapq
import sys

nums = [5, 1, 8, 3]
heapq.heapify(nums)                        # O(n)
heapq.heappush(nums, 0)                    # O(log n)
print(heapq.heappop(nums), nums[0])        # 0 1  (nums[0] is the smallest)
print(heapq.nlargest(2, [5, 1, 8, 3]))     # [8, 5]

max_heap = [-x for x in [5, 1, 8]]          # max-heap trick for any version: store negatives
heapq.heapify(max_heap)
print(-heapq.heappop(max_heap))            # 8

if sys.version_info >= (3, 14):            # Python 3.14 added real max-heap functions
    mh = [5, 1, 8]
    heapq.heapify_max(mh)
    print(heapq.heappop_max(mh))           # 8
```

* Ties compare the next tuple item: push `(priority, counter, item)` so items never get compared.

**bisect (binary search on a sorted list)**

* `bisect_left(a, x)`: first index where `x` could go (index of the first `x` if present).
* `bisect_right(a, x)`: index after the last `x`. `insort(a, x)`: insert keeping order (O(n) because of shifting).

**itertools and functools**

| Tool | Example |
|---|---|
| `product`, `permutations`, `combinations` | `combinations([1, 2, 3], 2)` -> (1,2), (1,3), (2,3) |
| `accumulate` | running sums: `accumulate([1, 2, 3])` -> 1, 3, 6 |
| `groupby` | groups **consecutive** equal keys (sort first) |
| `chain`, `islice`, `pairwise` (3.10+), `batched` (3.12+), `zip_longest` | combine / cut iterators |
| `functools.cache`, `lru_cache` | memoisation |
| `functools.partial` | pre-fill arguments |
| `functools.reduce`, `cmp_to_key` | fold; custom comparison sort |

**Other modules**: `math` (`gcd`, `lcm`, `isqrt`, `comb`, `perm`, `inf`), `random` (simulations, never for security),
`secrets` (tokens, passwords), `decimal`, `fractions`, `statistics`, `datetime` (use aware UTC:
`datetime.now(timezone.utc)`; `utcnow()` is deprecated), `zoneinfo`, `re` (`search` scans, `match` only at the start,
use raw strings, `.*?` is lazy), `logging` (levels DEBUG < INFO < WARNING < ERROR < CRITICAL), `argparse`,
`subprocess.run([...], check=True)` (pass a list, avoid `shell=True`), `json`, `csv`, `pathlib`.

---

## B8. Concurrency and async

| Workload | Best tool | Why |
|---|---|---|
| I/O-bound, few tasks (files, network, DB) | threads (`ThreadPoolExecutor`) | waiting releases the GIL |
| I/O-bound, thousands of connections | `asyncio` | very cheap tasks on one thread |
| CPU-bound pure Python | processes (`ProcessPoolExecutor`) | each process has its own interpreter |
| tiny tasks | none | the overhead is bigger than the gain |

* **GIL** (Global Interpreter Lock, CPython): only one thread runs Python bytecode at a time in the default build.
  It does **not** make `counter += 1` safe; use a `Lock`. Python 3.13 added an experimental free-threaded
  (no-GIL) build; in 3.14 it is officially supported but optional. The default build still has the GIL.
* Always call `future.result()` (or use `executor.map`) so exceptions are not lost.
* Share data with `queue.Queue`; avoid shared mutable state. Deadlock: always take locks in the same order.
* asyncio: `async def`, `await`, `asyncio.gather`, `asyncio.TaskGroup` (3.11+), `asyncio.timeout` (3.11+),
  `asyncio.to_thread` for blocking calls. Never call `time.sleep` inside async code; use `await asyncio.sleep`.
  Scripts start with `asyncio.run(main())`; Jupyter allows `await main()` directly.

---

## B9. Testing, quality and security

* Unit test = checks one small piece automatically. `unittest.TestCase` with `assertEqual`, `assertRaises`,
  `setUp`, `subTest`; or `pytest` with plain `assert`. Arrange -> Act -> Assert. Test edge and failure cases.
* `unittest.mock`: `Mock(return_value=...)`, `side_effect=Exception`, `patch("module.name")` (patch where the name is **looked up**).
* Quality tools: `ruff` (lint + format), `mypy` / `pyright` (types), `coverage`, pre-commit hooks.
* Performance: measure first (`timeit`, `cProfile`, `tracemalloc`), then fix the algorithm or data structure.

| Risk | Never | Instead |
|---|---|---|
| SQL injection | build SQL with f-strings | parameters: `cur.execute("... WHERE name = ?", (name,))` |
| Command injection | `shell=True` with user input | `subprocess.run(["ls", path])` |
| Code execution | `eval`, `pickle.load` on untrusted data | `ast.literal_eval`, `json` |
| Weak tokens | `random` | `secrets.token_hex()` |
| Passwords | plain text, MD5 | salted slow hash (`hashlib.scrypt`, `bcrypt`, `argon2`) |
| Secrets | keys in source code | environment variables / secrets manager |

---

## Self-test B

1. When should you use `@classmethod` instead of `@staticmethod`?
   <details><summary>Answer</summary>

   When the method needs the class: alternative constructors (`cls(...)` also works for subclasses) or class-wide data.
   A static method gets neither the object nor the class.
   </details>

2. What does `super()` really return in a diamond `class D(B, C)`?
   <details><summary>Answer</summary>

   A proxy for the **next class in D's MRO** (`D, B, C, A, object`). So inside `B`, `super()` can call `C`, not `A`.
   </details>

3. Why does a decorated function lose its name, and how do you fix it?
   <details><summary>Answer</summary>

   The decorator returns `wrapper`, so `__name__` and the docstring are the wrapper's. Use `@functools.wraps(func)`.
   </details>

4. What does this print?

   ```python
   gen = (x for x in range(3))
   print(list(gen), list(gen))
   ```

   <details><summary>Answer</summary>

   `[0, 1, 2] []`. A generator is one-shot; the second `list` gets nothing.
   </details>

5. Threads or processes for resizing 5,000 images in pure Python? For downloading 200 files?
   <details><summary>Answer</summary>

   Resizing is CPU-bound: processes (or a library that releases the GIL). Downloading is I/O-bound: threads or asyncio.
   </details>

6. What is wrong with `class Team: members = []`?
   <details><summary>Answer</summary>

   The list is a class attribute shared by every `Team`. Create `self.members = []` in `__init__`.
   </details>

7. You define `__eq__` in a class. Why can you no longer put objects in a set?
   <details><summary>Answer</summary>

   Defining `__eq__` sets `__hash__` to `None`. Also define `__hash__` (based on the same fields), or use `@dataclass(frozen=True)`.
   </details>

---
# Part C: Data Structures and Algorithms

## C1. How to solve an interview problem

```text
+---------------+   +----------------+   +----------------+   +---------------+
| 1. Understand |-->| 2. Clarify:    |-->| 3. Examples +  |-->| 4. Brute force|
|  restate it   |   |  input size,   |   |  edge cases    |   |  + its Big-O  |
+---------------+   |  sorted? dupes?|   +----------------+   +-------+-------+
                    +----------------+                                |
+---------------+   +----------------+   +----------------+   +-------v-------+
| 8. State time |<--| 7. Test: walk  |<--| 6. Code it     |<--| 5. Optimise:  |
|  and space    |   |  through cases |   |  cleanly       |   |  find pattern |
+---------------+   +----------------+   +----------------+   +---------------+
```

* Talk while you think. Interviewers grade problem solving, communication, code quality and testing, not only the answer.
* **Edge-case checklist**: empty input, one element, two elements, all equal, duplicates, negatives, zero,
  already sorted / reverse sorted, very large input, no valid answer.
* How to optimise a brute force:
  * Repeated searching -> **hash map / set**.
  * Sorted data or pairs -> **two pointers** or **binary search**.
  * Contiguous subarray / substring -> **sliding window** or **prefix sums**.
  * "Next greater", matching brackets -> **stack**.
  * Top k / smallest so far -> **heap**.
  * Overlapping subproblems -> **dynamic programming**.

**Debugging algorithm code**

```text
                       +-------------------+
                       | What went wrong?  |
                       +---------+---------+
          +----------------------+----------------------+
          v                      v                      v
+------------------+   +------------------+   +--------------------+
| Wrong answer     |   | Crash (error)    |   | Too slow           |
| - dry run with a |   | - read traceback |   | - count loops:     |
|   trace table    |   | - check indexes, |   |   nested? O(n^2)?  |
| - check edge     |   |   empty input,   |   | - x in list inside |
|   cases, off-by- |   |   None, base case|   |   a loop? use set  |
|   one, loop end  |   |                  |   | - repeated work?   |
| - compare with a |   |                  |   |   memoise / prefix |
|   brute force    |   |                  |   |   sums             |
+------------------+   +------------------+   +--------------------+
```

* Off-by-one checklist: is `stop` excluded in `range`/slices? `<` or `<=` in the loop? `mid + 1` or `mid`?
  Did you handle the last window / last group after the loop?
* Stress test: run your fast solution and a simple brute force on many random small inputs and compare.

```python
import random

def max_subarray_fast(nums):          # Kadane
    best = cur = nums[0]
    for x in nums[1:]:
        cur = max(x, cur + x)
        best = max(best, cur)
    return best

def max_subarray_brute(nums):
    return max(sum(nums[i:j]) for i in range(len(nums)) for j in range(i + 1, len(nums) + 1))

random.seed(0)
for _ in range(300):
    data = [random.randint(-5, 5) for _ in range(random.randint(1, 8))]
    assert max_subarray_fast(data) == max_subarray_brute(data), data
print("stress test passed")
```

---

## C2. Complexity analysis

| Big-O | Name | Example | Fine for n up to about |
|---|---|---|---|
| O(1) | constant | dict lookup, list index | any |
| O(log n) | logarithmic | binary search, heap push | any |
| O(n) | linear | one loop | 10^7 - 10^8 |
| O(n log n) | linearithmic | sorting | 10^6 |
| O(n^2) | quadratic | two nested loops | 10^4 |
| O(n^3) | cubic | three nested loops | 500 |
| O(2^n) | exponential | all subsets | 20 - 25 |
| O(n!) | factorial | all permutations | 10 |

* Read the constraints: `n <= 10^5` means you need about O(n log n) or better.
* Rules: drop constants (`3n + 5 = O(n)`); sequential steps add; nested loops multiply;
  halving each step gives `log n`.
* **Amortised O(1)**: `list.append` sometimes resizes (O(n)) but on average each append is O(1).
* **Space** counts extra memory, including the recursion stack (DFS on a chain of n nodes uses O(n) stack).
* Recursion cost = (number of calls) x (work per call). Naive Fibonacci: about 2^n calls. With memo: n calls.
* Python does roughly 10^7 simple operations per second; plan for that.

| Python operation | Time |
|---|---|
| `x in list`, `list.index`, `list.insert(0, x)`, `list.pop(0)` | O(n) |
| `x in set`, `x in dict`, `d[k]`, `s.add` | O(1) average |
| `list.append`, `list.pop()`, `deque.appendleft`, `deque.popleft` | O(1) |
| `sorted`, `list.sort` | O(n log n) |
| `heapq.heappush`, `heappop` | O(log n); `heapify` O(n) |
| slicing `a[i:j]`, `s + t`, `copy` | O(length) |
| `min`, `max`, `sum`, `len` | O(n), except `len` O(1) |

---

## C3. Math basics for DSA

| Tool | Meaning | Time |
|---|---|---|
| `a // b`, `a % b` | floor division, remainder | O(1) for normal sizes |
| `pow(a, b, m)` | `(a ** b) % m`, fast | O(log b) multiplications |
| `math.gcd(a, b)`, `math.lcm(a, b)` | greatest common divisor / least common multiple | O(log(min(a, b))) |
| `math.isqrt(n)` | exact integer square root (no float rounding errors) | about O(log n) steps on big ints; treat as cheap |
| `math.comb(n, k)`, `math.perm(n, k)`, `math.factorial(n)` | nCr, nPr, n! | depends on size |

* **Why `% (10**9 + 7)`?** Many problems have answers that are huge. The problem asks for the answer modulo a
  large prime so every language (with fixed-size integers) can give the same small number. Python ints never
  overflow, but you must still apply the modulo because the expected output is the remainder (and smaller
  numbers keep the code fast).
* Modular rules: `(a + b) % m == ((a % m) + (b % m)) % m`, `(a * b) % m == ((a % m) * (b % m)) % m`.
  Subtraction: `(a - b) % m` is always non-negative in Python.
* LCM: `a * b // math.gcd(a, b)` (or `math.lcm`).
* Sum 1..n: `n * (n + 1) // 2`. Arithmetic series of `k` terms: `k * (first + last) // 2` (use `//` to stay an int).
* Prime test: check divisors only up to `isqrt(n)`: O(sqrt n). Many primes: **sieve of Eratosthenes** O(n log log n).

```python
import math

def sieve(limit):
    is_prime = [True] * (limit + 1)
    is_prime[0:2] = [False, False]
    for p in range(2, math.isqrt(limit) + 1):
        if is_prime[p]:
            for multiple in range(p * p, limit + 1, p):
                is_prime[multiple] = False
    return [i for i, ok in enumerate(is_prime) if ok]

def gcd(a, b):                       # Euclid's algorithm
    while b:
        a, b = b, a % b
    return a

print(sieve(30))                     # [2, 3, 5, 7, 11, 13, 17, 19, 23, 29]
print(gcd(48, 18), math.lcm(4, 6), pow(2, 10, 1000))   # 6 12 24
```

---

## C4. Arrays, strings and hashing

* **Hash map patterns**: counting (`Counter`), "seen before?" (`set`), value -> index (`dict`), grouping by a key.
* **Prefix sums**: `prefix[i]` = sum of the first `i` items; sum of `nums[l:r]` = `prefix[r] - prefix[l]` in O(1).
* **Difference array**: add `v` to a range `[l, r]` in O(1): `diff[l] += v; diff[r + 1] -= v`, then take prefix sums.
* **Kadane**: best subarray sum ending here = `max(x, best_ending_before + x)`.

```python
from collections import defaultdict

def two_sum(nums, target):                 # value -> index, O(n)
    seen = {}
    for i, x in enumerate(nums):
        if target - x in seen:
            return [seen[target - x], i]
        seen[x] = i
    return []

def subarray_sum_equals_k(nums, k):        # prefix sums + hash map, works with negatives
    count, total, seen = 0, 0, {0: 1}
    for x in nums:
        total += x
        count += seen.get(total - k, 0)
        seen[total] = seen.get(total, 0) + 1
    return count

def group_anagrams(words):
    groups = defaultdict(list)
    for w in words:
        groups["".join(sorted(w))].append(w)
    return list(groups.values())

assert two_sum([2, 7, 11, 15], 9) == [0, 1]
assert subarray_sum_equals_k([1, 1, 1], 2) == 2
assert sorted(map(sorted, group_anagrams(["eat", "tea", "tan", "nat"]))) == [["eat", "tea"], ["nat", "tan"]]
print("hashing OK")
```

* Matrix moves: `for dr, dc in ((1, 0), (-1, 0), (0, 1), (0, -1)):` and check `0 <= r < rows and 0 <= c < cols`.
* Rotate a square matrix 90 degrees clockwise: `[list(row) for row in zip(*m[::-1])]`.
* Missing number in `0..n`: `n * (n + 1) // 2 - sum(nums)`, or XOR all indices and values (C18).

---

## C5. Two pointers

* **Opposite ends** (sorted array, palindromes, container with most water, 3Sum).
* **Same direction** (remove duplicates in place, move zeroes, merge sorted arrays): a "write" pointer and a "read" pointer.
* **Fast and slow** (linked list cycle, middle node).

```python
def pair_with_sum(sorted_nums, target):
    lo, hi = 0, len(sorted_nums) - 1
    while lo < hi:
        s = sorted_nums[lo] + sorted_nums[hi]
        if s == target:
            return lo, hi
        if s < target:
            lo += 1                   # need a bigger sum
        else:
            hi -= 1                   # need a smaller sum
    return None

def remove_duplicates(nums):          # in place, returns the new length
    write = 0
    for read in range(len(nums)):
        if read == 0 or nums[read] != nums[read - 1]:
            nums[write] = nums[read]
            write += 1
    return write

def trap_rain_water(h):
    lo, hi, left_max, right_max, water = 0, len(h) - 1, 0, 0, 0
    while lo < hi:
        if h[lo] < h[hi]:
            left_max = max(left_max, h[lo]); water += left_max - h[lo]; lo += 1
        else:
            right_max = max(right_max, h[hi]); water += right_max - h[hi]; hi -= 1
    return water

assert pair_with_sum([1, 3, 4, 6, 9], 10) == (0, 4)
data = [1, 1, 2, 3, 3]
assert remove_duplicates(data) == 3 and data[:3] == [1, 2, 3]
assert trap_rain_water([0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]) == 6
print("two pointers OK")
```

---

## C6. Sliding window

* Use for **contiguous** subarrays/substrings with a condition (longest, shortest, count).
* Fixed size `k`: add the new item, remove the item that left.
* Variable size: expand `right` every step; **shrink `left` while the window is invalid**; record the answer.
* If numbers can be negative and you need a sum, sliding window does not work; use prefix sums + hash map.

```text
  expand right --> [ l . . . . r ] --> invalid? --> move l right until valid --> update answer
```

```python
from collections import Counter

def longest_unique_substring(s):
    seen, left, best = set(), 0, 0
    for right, ch in enumerate(s):
        while ch in seen:                 # window invalid: shrink from the left
            seen.remove(s[left])
            left += 1
        seen.add(ch)                      # expand
        best = max(best, right - left + 1)
    return best

def min_window(s, t):                     # smallest window containing all of t
    need, missing = Counter(t), len(t)
    left, best = 0, ""
    for right, ch in enumerate(s):
        if need[ch] > 0:
            missing -= 1
        need[ch] -= 1
        while missing == 0:
            if not best or right - left + 1 < len(best):
                best = s[left:right + 1]
            need[s[left]] += 1
            if need[s[left]] > 0:
                missing += 1
            left += 1
    return best

def max_sum_k(nums, k):                   # fixed window
    window = best = sum(nums[:k])
    for i in range(k, len(nums)):
        window += nums[i] - nums[i - k]
        best = max(best, window)
    return best

assert [longest_unique_substring(s) for s in ("abcabcbb", "bbbb", "")] == [3, 1, 0]
assert min_window("ADOBECODEBANC", "ABC") == "BANC"
assert max_sum_k([2, 1, 5, 1, 3, 2], 3) == 9
print("sliding window OK")
```

---

## C7. Recursion and backtracking

* Recursion recipe: (1) base case, (2) make the problem smaller, (3) trust the recursive call, (4) combine.
* **Backtracking** = choose -> explore -> un-choose. Prune branches that cannot succeed.
* Always store a **copy** of the path: `result.append(path[:])`.

```text
                    []
          /          |          \
       [1]          [2]         [3]          subsets: every node is an answer
      /    \          |
  [1,2]   [1,3]     [2,3]
    |
 [1,2,3]
```

```python
def subsets(nums):
    result, path = [], []
    def backtrack(start):
        result.append(path[:])
        for i in range(start, len(nums)):
            path.append(nums[i])          # choose
            backtrack(i + 1)              # explore
            path.pop()                    # un-choose
    backtrack(0)
    return result

def permutations(nums):
    result, path, used = [], [], [False] * len(nums)
    def backtrack():
        if len(path) == len(nums):
            result.append(path[:]); return
        for i, x in enumerate(nums):
            if not used[i]:
                used[i] = True; path.append(x)
                backtrack()
                path.pop(); used[i] = False
    backtrack()
    return result

def combination_sum(candidates, target):  # numbers may be reused
    result, path = [], []
    def backtrack(start, remaining):
        if remaining == 0:
            result.append(path[:]); return
        for i in range(start, len(candidates)):
            if candidates[i] <= remaining:   # prune
                path.append(candidates[i])
                backtrack(i, remaining - candidates[i])
                path.pop()
    backtrack(0, target)
    return result

assert len(subsets([1, 2, 3])) == 8 and len(permutations([1, 2, 3])) == 6
assert combination_sum([2, 3, 6, 7], 7) == [[2, 2, 3], [7]]
print("backtracking OK")
```

* Complexity: subsets O(n * 2^n), permutations O(n * n!). Duplicates in input: sort, then skip
  `if i > start and nums[i] == nums[i - 1]: continue`.
* Classic problems: subsets I/II, permutations I/II, combinations, combination sum I/II, palindrome partitioning,
  letter combinations of a phone number, generate parentheses, N-Queens, word search, sudoku solver.

---

## C8. Sorting

| Algorithm | Best | Average | Worst | Extra space | Stable |
|---|---|---|---|---|---|
| Bubble / Insertion | O(n) | O(n^2) | O(n^2) | O(1) | Yes |
| Selection | O(n^2) | O(n^2) | O(n^2) | O(1) | No |
| Merge sort | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| Quick sort | O(n log n) | O(n log n) | O(n^2) | O(log n) | No |
| Heap sort | O(n log n) | O(n log n) | O(n log n) | O(1) | No |
| Counting sort | O(n + k) | O(n + k) | O(n + k) | O(k) | Yes |
| Timsort (Python) | O(n) | O(n log n) | O(n log n) | O(n) | Yes |

* **Stable** = equal items keep their original order. Python's `sorted`/`sort` are stable.
* Custom order: `key=` (preferred) or `functools.cmp_to_key` for pairwise rules (e.g. "largest number").
* **Quickselect** finds the k-th smallest in O(n) average (O(n^2) worst).

```python
import random
from functools import cmp_to_key

def merge_sort(a):
    if len(a) <= 1:
        return a
    mid = len(a) // 2
    left, right = merge_sort(a[:mid]), merge_sort(a[mid:])
    merged, i, j = [], 0, 0
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:           # <= keeps it stable
            merged.append(left[i]); i += 1
        else:
            merged.append(right[j]); j += 1
    return merged + left[i:] + right[j:]

def quick_sort(a):
    if len(a) <= 1:
        return a
    pivot = random.choice(a)              # random pivot avoids the O(n^2) worst case on sorted input
    return (quick_sort([x for x in a if x < pivot]) + [x for x in a if x == pivot]
            + quick_sort([x for x in a if x > pivot]))

def largest_number(nums):
    order = lambda a, b: -1 if a + b > b + a else (1 if a + b < b + a else 0)
    s = "".join(sorted(map(str, nums), key=cmp_to_key(order)))
    return "0" if s[0] == "0" else s

random.seed(1)
data = [random.randint(-50, 50) for _ in range(40)]
assert merge_sort(data) == sorted(data) == quick_sort(data)
assert largest_number([3, 30, 34, 5, 9]) == "9534330"
print("sorting OK")
```

---

## C9. Binary search

* Works on sorted data, or any **monotonic** condition (false, false, ..., true, true).
* Template "first index where `condition(i)` is true" (lower bound) avoids most off-by-one bugs:

```python
def first_true(lo, hi, condition):        # search in [lo, hi); returns hi if never true
    while lo < hi:
        mid = (lo + hi) // 2
        if condition(mid):
            hi = mid                      # mid might be the answer; keep it
        else:
            lo = mid + 1                  # mid is not the answer
    return lo

def search_rotated(nums, target):
    lo, hi = 0, len(nums) - 1
    while lo <= hi:
        mid = (lo + hi) // 2
        if nums[mid] == target:
            return mid
        if nums[lo] <= nums[mid]:         # left half is sorted
            if nums[lo] <= target < nums[mid]:
                hi = mid - 1
            else:
                lo = mid + 1
        else:                             # right half is sorted
            if nums[mid] < target <= nums[hi]:
                lo = mid + 1
            else:
                hi = mid - 1
    return -1

def min_eating_speed(piles, hours):       # binary search on the answer
    return first_true(1, max(piles) + 1, lambda k: sum((p + k - 1) // k for p in piles) <= hours)

a = [1, 3, 3, 3, 7]
assert first_true(0, len(a), lambda i: a[i] >= 3) == 1     # first 3
assert first_true(0, len(a), lambda i: a[i] > 3) == 4      # after the last 3
assert search_rotated([4, 5, 6, 7, 0, 1, 2], 0) == 4 and search_rotated([1], 2) == -1
assert min_eating_speed([3, 6, 7, 11], 8) == 4
print("binary search OK")
```

* Library: `bisect.bisect_left(a, x)` / `bisect_right(a, x)` (with `key=` since 3.10).
* Classic problems: first/last position, search insert position, rotated array (search, minimum), peak element,
  search a 2D matrix, Koko eating bananas, ship packages in D days, median of two sorted arrays.

---

## C10. Linked lists

* Each node has `val` and `next`. No index access: reaching position `i` is O(i).
* **Dummy node**: start with `dummy = ListNode(0)` so the head is never a special case; return `dummy.next`.
* **Fast/slow pointers**: middle (slow at the middle when fast reaches the end), cycle detection (they meet).

```text
reverse:   None <- 1    2 -> 3 -> None
                  prev  cur
           each step: nxt = cur.next; cur.next = prev; prev = cur; cur = nxt
```

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val, self.next = val, next

def build(values):
    dummy = tail = ListNode()
    for v in values:
        tail.next = ListNode(v); tail = tail.next
    return dummy.next

def to_list(node):
    out = []
    while node:
        out.append(node.val); node = node.next
    return out

def reverse(head):
    prev, cur = None, head
    while cur:
        cur.next, prev, cur = prev, cur, cur.next
    return prev

def merge_two(a, b):
    dummy = tail = ListNode()
    while a and b:
        if a.val <= b.val:
            tail.next, a = a, a.next
        else:
            tail.next, b = b, b.next
        tail = tail.next
    tail.next = a or b
    return dummy.next

def middle(head):
    slow = fast = head
    while fast and fast.next:
        slow, fast = slow.next, fast.next.next
    return slow

def has_cycle(head):
    slow = fast = head
    while fast and fast.next:
        slow, fast = slow.next, fast.next.next
        if slow is fast:
            return True
    return False

assert to_list(reverse(build([1, 2, 3]))) == [3, 2, 1] and reverse(None) is None
assert to_list(merge_two(build([1, 3]), build([2, 4]))) == [1, 2, 3, 4]
assert middle(build([1, 2, 3, 4, 5])).val == 3
loop = build([1, 2, 3]); loop.next.next.next = loop
assert has_cycle(loop) and not has_cycle(build([1, 2]))
print("linked list OK")
```

* Classic problems: reverse (also in groups of k), merge two/k sorted lists, remove n-th node from end (gap of n),
  cycle start, palindrome list, reorder list, add two numbers, intersection, LRU cache (dict + doubly linked list),
  copy list with random pointer.

---

## C11. Stacks and queues

* **Stack** (last in, first out): Python `list` with `append` / `pop`. Use for matching brackets, undo, DFS, expression evaluation.
* **Queue** (first in, first out): `collections.deque` with `append` / `popleft`. Use for BFS, scheduling.
* **Monotonic stack**: keeps items in increasing or decreasing order to answer "next greater/smaller element" in O(n).
* **Monotonic deque**: sliding window maximum in O(n).

```python
from collections import deque

def is_valid(s):
    pairs, stack = {")": "(", "]": "[", "}": "{"}, []
    for ch in s:
        if ch in "([{":
            stack.append(ch)
        elif not stack or stack.pop() != pairs[ch]:
            return False
    return not stack

def next_greater(nums):                   # -1 when there is none
    answer, stack = [-1] * len(nums), []  # stack holds indexes waiting for an answer
    for i, x in enumerate(nums):
        while stack and nums[stack[-1]] < x:
            answer[stack.pop()] = x
        stack.append(i)
    return answer

def sliding_max(nums, k):
    dq, out = deque(), []                 # indexes, values decreasing from front to back
    for i, x in enumerate(nums):
        while dq and nums[dq[-1]] <= x:
            dq.pop()
        dq.append(i)
        if dq[0] <= i - k:
            dq.popleft()                  # front left the window
        if i >= k - 1:
            out.append(nums[dq[0]])
    return out

assert is_valid("([]{})") and not is_valid("(]") and not is_valid("((")
assert next_greater([2, 1, 2, 4, 3]) == [4, 2, 4, -1, -1]
assert sliding_max([1, 3, -1, -3, 5, 3, 6, 7], 3) == [3, 3, 5, 5, 6, 7]
print("stack and queue OK")
```

* Classic problems: valid parentheses, min stack, evaluate reverse Polish notation, decode string, daily temperatures,
  largest rectangle in histogram, queue using two stacks, sliding window maximum.

---

## C12. Heaps (priority queues)

* A min-heap keeps the smallest item at index 0. Stored as a list: children of `i` are `2i + 1` and `2i + 2`; parent is `(i - 1) // 2`.
* Push/pop O(log n), peek O(1), heapify O(n).
* **Top k largest**: keep a **min-heap of size k** (pop when size > k) -> O(n log k).
* **Median of a stream**: max-heap for the lower half, min-heap for the upper half.

```python
import heapq

def kth_largest(nums, k):
    heap = []
    for x in nums:
        heapq.heappush(heap, x)
        if len(heap) > k:
            heapq.heappop(heap)           # remove the smallest; the k largest remain
    return heap[0]

def merge_k_sorted(lists):
    heap = [(lst[0], i, 0) for i, lst in enumerate(lists) if lst]
    heapq.heapify(heap)
    out = []
    while heap:
        val, i, j = heapq.heappop(heap)
        out.append(val)
        if j + 1 < len(lists[i]):
            heapq.heappush(heap, (lists[i][j + 1], i, j + 1))
    return out

class MedianFinder:
    def __init__(self):
        self.low, self.high = [], []      # low is a max-heap (negated), high is a min-heap
    def add(self, x):
        heapq.heappush(self.low, -x)
        heapq.heappush(self.high, -heapq.heappop(self.low))
        if len(self.high) > len(self.low):
            heapq.heappush(self.low, -heapq.heappop(self.high))
    def median(self):
        if len(self.low) > len(self.high):
            return -self.low[0]
        return (-self.low[0] + self.high[0]) / 2

assert kth_largest([3, 2, 1, 5, 6, 4], 2) == 5
assert merge_k_sorted([[1, 4], [2, 5], [], [0]]) == [0, 1, 2, 4, 5]
mf = MedianFinder()
for v in [5, 2, 8]:
    mf.add(v)
assert mf.median() == 5
print("heap OK")
```

* Classic problems: kth largest, top k frequent, k closest points, merge k sorted lists, median from data stream,
  task scheduler, reorganize string, meeting rooms II.

---

## C13. Trees and binary search trees

* Terms: root, parent, child, leaf, height (longest path down), depth (distance from root), subtree.
* Traversals: **preorder** (node, left, right), **inorder** (left, node, right; gives sorted order in a BST),
  **postorder** (left, right, node), **level order** (BFS with a queue).
* Most tree problems: "what do I need from the left and right subtrees?" -> recursive DFS that returns that.
* **BST rule**: everything in the left subtree < node < everything in the right subtree.
  Search/insert/delete are O(h): O(log n) if balanced, O(n) if skewed.

```text
        4          preorder : 4 2 1 3 6
       / \         inorder  : 1 2 3 4 6   (sorted, because it is a BST)
      2   6        postorder: 1 3 2 6 4
     / \           level    : [4] [2, 6] [1, 3]
    1   3
```

```python
from collections import deque

class TreeNode:
    def __init__(self, val, left=None, right=None):
        self.val, self.left, self.right = val, left, right

def inorder(node):
    return inorder(node.left) + [node.val] + inorder(node.right) if node else []

def inorder_iterative(root):
    out, stack, node = [], [], root
    while stack or node:
        while node:                       # go left as far as possible
            stack.append(node); node = node.left
        node = stack.pop()
        out.append(node.val)
        node = node.right
    return out

def level_order(root):
    levels, q = [], deque([root] if root else [])
    while q:
        level = []
        for _ in range(len(q)):
            node = q.popleft()
            level.append(node.val)
            q.extend(child for child in (node.left, node.right) if child)
        levels.append(level)
    return levels

def max_depth(node):
    return 0 if node is None else 1 + max(max_depth(node.left), max_depth(node.right))

def is_valid_bst(node, low=float("-inf"), high=float("inf")):
    if node is None:
        return True
    if not low < node.val < high:
        return False
    return is_valid_bst(node.left, low, node.val) and is_valid_bst(node.right, node.val, high)

def lca(root, p, q):                      # lowest common ancestor in a binary tree
    if root is None or root.val in (p, q):
        return root
    left, right = lca(root.left, p, q), lca(root.right, p, q)
    return root if left and right else left or right

root = TreeNode(4, TreeNode(2, TreeNode(1), TreeNode(3)), TreeNode(6))
assert inorder(root) == inorder_iterative(root) == [1, 2, 3, 4, 6]
assert level_order(root) == [[4], [2, 6], [1, 3]] and max_depth(root) == 3
assert is_valid_bst(root) and not is_valid_bst(TreeNode(5, TreeNode(6)))
assert lca(root, 1, 3).val == 2 and lca(root, 1, 6).val == 4
print("trees OK")
```

* Classic problems: max depth, diameter, balanced tree, same / symmetric / invert tree, path sum, right side view,
  LCA, serialize and deserialize, build from preorder + inorder, validate BST, kth smallest in BST, BST insert/delete.

---

## C14. Tries (prefix trees)

* Each node is a dict of children plus an "end of word" flag. Insert/search cost O(length of the word).
* Use for prefix search, autocomplete, word games (word search II), longest common prefix.

```python
class Trie:
    def __init__(self):
        self.root = {}

    def insert(self, word):
        node = self.root
        for ch in word:
            node = node.setdefault(ch, {})
        node["$"] = True                  # end-of-word marker

    def _walk(self, text):
        node = self.root
        for ch in text:
            if ch not in node:
                return None
            node = node[ch]
        return node

    def search(self, word):
        node = self._walk(word)
        return node is not None and "$" in node

    def starts_with(self, prefix):
        return self._walk(prefix) is not None

t = Trie()
for w in ["apple", "app", "bat"]:
    t.insert(w)
assert t.search("app") and not t.search("ap") and t.starts_with("ap") and not t.starts_with("c")
print("trie OK")
```

---

## C15. Graphs

* Representations: **adjacency list** `{node: [neighbours]}` (usual choice), adjacency matrix, edge list. A grid is a graph
  where each cell connects to its 4 neighbours.
* **BFS** (queue): shortest path in an **unweighted** graph, level by level. Mark visited **when you add to the queue**.
* **DFS** (recursion or stack): connected components, cycle detection, paths, topological sort.
* **Topological sort** (DAG, e.g. course schedule): Kahn's algorithm with in-degrees. If not all nodes are output, there is a cycle.
* **Dijkstra**: shortest paths with non-negative weights, using a heap: O((V + E) log V).
  Negative weights: Bellman-Ford O(V * E).
* **Union-Find (DSU)**: merge groups and ask "same group?" in almost O(1). Use for components, redundant edge, Kruskal's MST.
* Complexity of BFS / DFS: O(V + E).

```python
import heapq
from collections import deque

def bfs_shortest(graph, start, goal):
    dist, q = {start: 0}, deque([start])
    while q:
        node = q.popleft()
        if node == goal:
            return dist[node]
        for nxt in graph.get(node, []):
            if nxt not in dist:           # visited check when enqueuing
                dist[nxt] = dist[node] + 1
                q.append(nxt)
    return -1

def num_islands(grid):
    rows, cols, seen, count = len(grid), len(grid[0]) if grid else 0, set(), 0
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == "1" and (r, c) not in seen:
                count += 1
                stack = [(r, c)]; seen.add((r, c))
                while stack:              # iterative DFS (no recursion limit problems)
                    cr, cc = stack.pop()
                    for nr, nc in ((cr + 1, cc), (cr - 1, cc), (cr, cc + 1), (cr, cc - 1)):
                        if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] == "1" and (nr, nc) not in seen:
                            seen.add((nr, nc)); stack.append((nr, nc))
    return count

def topo_sort(n, edges):                  # edges: (before, after); returns [] if there is a cycle
    graph, indeg = {i: [] for i in range(n)}, [0] * n
    for a, b in edges:
        graph[a].append(b); indeg[b] += 1
    q = deque(i for i in range(n) if indeg[i] == 0)
    order = []
    while q:
        node = q.popleft(); order.append(node)
        for nxt in graph[node]:
            indeg[nxt] -= 1
            if indeg[nxt] == 0:
                q.append(nxt)
    return order if len(order) == n else []

def dijkstra(graph, src):                 # graph: {u: [(v, weight), ...]}
    dist, heap = {src: 0}, [(0, src)]
    while heap:
        d, u = heapq.heappop(heap)
        if d > dist[u]:
            continue                      # stale entry
        for v, w in graph.get(u, []):
            if d + w < dist.get(v, float("inf")):
                dist[v] = d + w
                heapq.heappush(heap, (d + w, v))
    return dist

class DSU:
    def __init__(self, n):
        self.parent, self.size = list(range(n)), [1] * n
    def find(self, x):
        while self.parent[x] != x:
            self.parent[x] = self.parent[self.parent[x]]   # path compression
            x = self.parent[x]
        return x
    def union(self, a, b):
        ra, rb = self.find(a), self.find(b)
        if ra == rb:
            return False                  # already connected: this edge makes a cycle
        if self.size[ra] < self.size[rb]:
            ra, rb = rb, ra
        self.parent[rb] = ra; self.size[ra] += self.size[rb]
        return True

g = {"A": ["B", "C"], "B": ["D"], "C": ["D"], "D": []}
assert bfs_shortest(g, "A", "D") == 2 and bfs_shortest(g, "D", "A") == -1
assert num_islands(["110", "010", "001"]) == 2 and num_islands([]) == 0
assert topo_sort(3, [(0, 1), (1, 2)]) == [0, 1, 2] and topo_sort(2, [(0, 1), (1, 0)]) == []
assert dijkstra({"a": [("b", 4), ("c", 1)], "c": [("b", 2)]}, "a") == {"a": 0, "b": 3, "c": 1}
dsu = DSU(4)
assert dsu.union(0, 1) and dsu.union(1, 2) and not dsu.union(0, 2) and dsu.find(3) == 3
print("graphs OK")
```

* Cycle in a **directed** graph: DFS with 3 colours (white = unvisited, grey = on the current path, black = done);
  reaching a grey node means a cycle. In an **undirected** graph: union-find, or DFS ignoring the parent.
* Classic problems: number of islands, clone graph, course schedule I/II, rotting oranges (multi-source BFS),
  word ladder, network delay time (Dijkstra), cheapest flights within k stops, redundant connection,
  number of provinces, min cost to connect points (MST), bipartite graph, Pacific Atlantic water flow.

---

## C16. Greedy and intervals

* **Greedy**: take the best local choice and never undo it. It works only when you can argue that the greedy choice
  is never worse (exchange argument). If greedy fails (e.g. coins `[1, 3, 4]`, amount 6: greedy gives 4+1+1, best is 3+3), use DP.
* **Intervals**: sort by start (merging) or by end (choosing the most non-overlapping intervals).
* Meeting rooms needed = maximum overlap: sort starts and ends, or use a min-heap of end times.

```python
import heapq

def merge_intervals(intervals):
    merged = []
    for start, end in sorted(intervals):
        if merged and start <= merged[-1][1]:
            merged[-1][1] = max(merged[-1][1], end)
        else:
            merged.append([start, end])
    return merged

def min_meeting_rooms(intervals):
    ends = []
    for start, end in sorted(intervals):
        if ends and ends[0] <= start:
            heapq.heapreplace(ends, end)  # reuse the room that frees up first
        else:
            heapq.heappush(ends, end)
    return len(ends)

def can_jump(nums):
    reach = 0
    for i, step in enumerate(nums):
        if i > reach:
            return False
        reach = max(reach, i + step)
    return True

assert merge_intervals([[1, 3], [8, 10], [2, 6]]) == [[1, 6], [8, 10]]
assert min_meeting_rooms([(0, 30), (5, 10), (15, 20)]) == 2
assert can_jump([2, 3, 1, 1, 4]) and not can_jump([3, 2, 1, 0, 4])
print("greedy OK")
```

* Classic problems: jump game I/II, gas station, partition labels, non-overlapping intervals, insert interval,
  minimum arrows to burst balloons, assign cookies, best time to buy and sell stock II.

---

## C17. Dynamic programming

* Use DP when a problem has **overlapping subproblems** (the same small question is asked many times) and
  **optimal substructure** (the best answer is built from best answers to smaller parts).
* Signals: "number of ways", "minimum/maximum cost", "is it possible", "longest/shortest ...", with choices at each step.

```text
+-------------+   +---------------+   +-------------+   +-------------+   +-------------+
| 1. State:   |-->| 2. Transition |-->| 3. Base     |-->| 4. Order of |-->| 5. Answer   |
| what dp[i]  |   | dp[i] from    |   | cases       |   | filling the |   | which cell? |
| means       |   | smaller states|   |             |   | table       |   | then reduce |
+-------------+   +---------------+   +-------------+   +-------------+   |  space      |
                                                                          +-------------+
```

* **Top-down** (recursion + memo, `@functools.cache`) is easier to write; **bottom-up** (table) avoids recursion limits
  and often allows saving space (keep only the last row).
* Debug DP: print the table for a tiny input, check the base cases, check the loop order (do you read cells that are already filled?).

| Problem | State | Transition |
|---|---|---|
| Climbing stairs | `dp[i]` = ways to reach step i | `dp[i-1] + dp[i-2]` |
| House robber | best up to house i | `max(dp[i-1], dp[i-2] + nums[i])` |
| Coin change (min coins) | min coins for amount a | `1 + min(dp[a - c])` |
| Coin change (ways) | ways to make a | `dp[a] += dp[a - c]` (coins in the outer loop) |
| Longest increasing subsequence | LIS ending at i | `1 + max(dp[j])` for `j < i`, `nums[j] < nums[i]`; O(n log n) with bisect |
| Unique paths | paths to (r, c) | `dp[r-1][c] + dp[r][c-1]` |
| Longest common subsequence | LCS of `a[:i]`, `b[:j]` | equal: `dp[i-1][j-1] + 1`, else `max(dp[i-1][j], dp[i][j-1])` |
| Edit distance | edits for `a[:i]` -> `b[:j]` | equal: `dp[i-1][j-1]`, else `1 + min(insert, delete, replace)` |
| 0/1 knapsack | best value with capacity w | `max(dp[w], dp[w - wt] + val)`, loop w **downwards** |
| Word break | can `s[:i]` be split | any `dp[j] and s[j:i] in words` |

```python
from bisect import bisect_left
from functools import cache

def coin_change(coins, amount):
    INF = float("inf")
    dp = [0] + [INF] * amount
    for a in range(1, amount + 1):
        for c in coins:
            if c <= a:
                dp[a] = min(dp[a], dp[a - c] + 1)
    return -1 if dp[amount] == INF else dp[amount]

def lcs(a, b):
    dp = [[0] * (len(b) + 1) for _ in range(len(a) + 1)]
    for i in range(1, len(a) + 1):
        for j in range(1, len(b) + 1):
            if a[i - 1] == b[j - 1]:
                dp[i][j] = dp[i - 1][j - 1] + 1
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])
    return dp[-1][-1]

def edit_distance(a, b):
    @cache
    def solve(i, j):                      # top-down version
        if i == len(a):
            return len(b) - j
        if j == len(b):
            return len(a) - i
        if a[i] == b[j]:
            return solve(i + 1, j + 1)
        return 1 + min(solve(i + 1, j), solve(i, j + 1), solve(i + 1, j + 1))
    return solve(0, 0)

def knapsack(weights, values, capacity):
    dp = [0] * (capacity + 1)
    for wt, val in zip(weights, values):
        for w in range(capacity, wt - 1, -1):   # downwards: each item used at most once
            dp[w] = max(dp[w], dp[w - wt] + val)
    return dp[capacity]

def lis_length(nums):                     # O(n log n): tails[k] = smallest tail of an increasing run of length k+1
    tails = []
    for x in nums:
        i = bisect_left(tails, x)
        if i == len(tails):
            tails.append(x)
        else:
            tails[i] = x
    return len(tails)

assert coin_change([1, 2, 5], 11) == 3 and coin_change([2], 3) == -1 and coin_change([1, 3, 4], 6) == 2
assert lcs("abcde", "ace") == 3 and edit_distance("horse", "ros") == 3
assert knapsack([1, 3, 4], [15, 20, 30], 4) == 35
assert lis_length([10, 9, 2, 5, 3, 7, 101, 18]) == 4 and lis_length([]) == 0
print("dynamic programming OK")
```

```text
LCS table for "ace" (rows) vs "abcde" (columns)
        ""  a  b  c  d  e
    ""   0  0  0  0  0  0
    a    0  1  1  1  1  1
    c    0  1  1  2  2  2
    e    0  1  1  2  2  3     answer = bottom-right cell = 3
```

* Classic problems: climbing stairs, house robber I/II, coin change I/II, decode ways, word break, LIS,
  maximum product subarray, unique paths, minimum path sum, LCS, edit distance, partition equal subset sum,
  target sum, longest palindromic substring/subsequence, burst balloons.

---

## C18. Bit manipulation

| Task | Code |
|---|---|
| is bit i set? | `(x >> i) & 1` |
| set / clear / toggle bit i | `x \| (1 << i)`, `x & ~(1 << i)`, `x ^ (1 << i)` |
| lowest set bit | `x & -x` |
| remove lowest set bit | `x & (x - 1)` |
| power of two? | `x > 0 and x & (x - 1) == 0` |
| count set bits | `bin(x).count("1")` or `x.bit_count()` (3.10+) |
| XOR facts | `a ^ a == 0`, `a ^ 0 == a`, order does not matter |

```python
from functools import reduce
from operator import xor

def single_number(nums):                  # every number appears twice except one
    return reduce(xor, nums, 0)

def missing_number(nums):                 # numbers 0..n with one missing
    result = len(nums)
    for i, x in enumerate(nums):
        result ^= i ^ x
    return result

def subsets_bitmask(items):
    n = len(items)
    return [[items[i] for i in range(n) if mask >> i & 1] for mask in range(1 << n)]

assert single_number([4, 1, 2, 1, 2]) == 4
assert missing_number([3, 0, 1]) == 2
assert len(subsets_bitmask(["a", "b", "c"])) == 8
assert (12).bit_count() == 2 and 12 & -12 == 4
print("bits OK")
```

---

## Self-test C

1. Constraints say `n <= 10^5`. Is an O(n^2) solution acceptable?
   <details><summary>Answer</summary>

   No. 10^10 operations is far too slow. Aim for O(n log n) or O(n).
   </details>

2. Longest subarray with sum `k` when numbers can be negative: sliding window or prefix sums?
   <details><summary>Answer</summary>

   Prefix sums + hash map (store the first index of each prefix sum). Sliding window needs a condition that only
   gets "more true" as the window grows, which negatives break.
   </details>

3. Why mark a node as visited when it is added to the BFS queue, not when it is removed?
   <details><summary>Answer</summary>

   Otherwise the same node can be added many times before it is processed, wasting time and memory (and giving wrong counts).
   </details>

4. Why does the 0/1 knapsack loop go downwards over the capacity?
   <details><summary>Answer</summary>

   Going downwards reads `dp[w - wt]` values from the previous item, so each item is used at most once.
   Going upwards would allow reusing the same item (that is the unbounded knapsack).
   </details>

5. What is the time complexity of building a heap with `heapify`, and of popping all items?
   <details><summary>Answer</summary>

   `heapify` is O(n). Popping all n items is O(n log n).
   </details>

6. You need the k-th largest element of an unsorted array. Give two approaches and their costs.
   <details><summary>Answer</summary>

   Min-heap of size k: O(n log k). Quickselect: O(n) average, O(n^2) worst. (Sorting: O(n log n).)
   </details>

7. When does greedy fail for coin change? What do you use instead?
   <details><summary>Answer</summary>

   With coins like `[1, 3, 4]` and amount 6, greedy takes 4+1+1 (3 coins) but 3+3 (2 coins) is better. Use DP.
   </details>

8. How do you detect a cycle in a directed graph?
   <details><summary>Answer</summary>

   DFS with three colours (reaching a node that is still on the current path means a cycle), or Kahn's algorithm:
   if the topological order has fewer than n nodes, there is a cycle.
   </details>

---
# Part D: Final Revision

## D1. Pattern recognition sheet

| If the problem says... | Think of | Typical cost |
|---|---|---|
| "two numbers that sum to", "seen before", "count frequency" | hash map / set | O(n) |
| sorted array, pairs/triples, palindrome, "in place" | two pointers | O(n) |
| longest/shortest **contiguous** subarray or substring | sliding window | O(n) |
| subarray sum equals k (negatives allowed), range sums | prefix sums + hash map | O(n) |
| sorted data, "minimum value such that...", "maximum that still works" | binary search (on index or on answer) | O(log n) per check |
| matching brackets, "next greater/smaller", undo | stack / monotonic stack | O(n) |
| sliding window max/min | monotonic deque | O(n) |
| top k, k-th largest, merge k sorted, running median | heap | O(n log k) |
| all subsets, permutations, combinations, "generate all" | backtracking | exponential |
| shortest path, unweighted, "minimum steps" | BFS | O(V + E) |
| shortest path with weights >= 0 | Dijkstra | O(E log V) |
| dependencies, ordering, "can all courses be finished" | topological sort | O(V + E) |
| connected groups, "are they connected", redundant edge | union-find or DFS | about O(n) |
| prefix search, autocomplete, many words | trie | O(word length) |
| intervals, meetings, overlaps | sort + sweep, heap of end times | O(n log n) |
| "number of ways", "min/max cost", choices at each step | dynamic programming | states x transitions |
| "each element appears twice except one", subsets of small n | bit manipulation | O(n) |
| linked list middle, cycle, k-th from end | fast/slow pointers, gap pointers | O(n) |
| tree: depth, diameter, path sums, LCA | DFS returning values from children | O(n) |
| tree level by level, right side view | BFS by levels | O(n) |

---

## D2. Python gotchas: predict the output

Cover the answer, predict, then check.

| Code | Output | Why |
|---|---|---|
| `print(0.1 + 0.2 == 0.3)` | `False` | floats are approximate |
| `print(round(2.5), round(3.5))` | `2 4` | round half to even |
| `print(-7 // 2, -7 % 3)` | `-4 2` | floor division |
| `print(bool("False"), bool([]), bool([0]))` | `True False True` | non-empty is truthy |
| `print(1 == 1.0 == True)` | `True` | equal values (and equal hashes) |
| `d = {1: "a", 1.0: "b", True: "c"}; print(d)` | `{1: 'c'}` | the three keys are equal |
| `a = [1, 2]; b = a; b += [3]; print(a)` | `[1, 2, 3]` | `+=` mutates the shared list |
| `t = (1, [2]); t[1].append(3); print(t)` | `(1, [2, 3])` | tuple immutability is shallow |
| `print([] == [], [] is [])` | `True False` | equal values, different objects |
| `print("abc"[5:], "abc"[-1])` | ` c` (empty string, then `c`) | slices never raise |
| `x = [1, 2, 3]; print(x.append(4))` | `None` | in-place methods return `None` |
| `print(any([]), all([]))` | `False True` | empty-collection rules |
| `print(sorted("bBa"))` | `['B', 'a', 'b']` | uppercase sorts first |
| `print(type({}), type(set()))` | `<class 'dict'> <class 'set'>` | `{}` is a dict |
| `print([i for i in range(3)][-1], list(range(5, 0, -2)))` | `2 [5, 3, 1]` | stop is excluded |
| `fs = [lambda: i for i in range(3)]; print([f() for f in fs])` | `[2, 2, 2]` | late binding |
| `print("a" * 3 + "b" * 0)` | `aaa` | repetition |
| `print(int("10", 2), int(3.9), int(-3.9))` | `2 3 -3` | base 2; truncation toward zero |
| `print(len("café".encode()))` | `5` | `é` takes 2 bytes in UTF-8 |
| `print(max([], default=-1), sum([]))` | `-1 0` | safe empty handling |

---

## D3. Debugging checklist

* Read the **last line** of the traceback first (error type + message), then the line numbers above it.
* Reproduce with the **smallest input** that fails.
* Print the values at the failing line: `print(f"{i=} {lo=} {hi=} {window=}")`, or step with the debugger (`breakpoint()`).
* Check the usual suspects:
  * off-by-one (`range` stop, `<` vs `<=`, `mid` vs `mid + 1`)
  * empty input / single element / `None`
  * a function that returns `None` (`sort`, `append`, missing `return`)
  * shared mutable objects (`b = a`, `[[0] * n] * m`, mutable default arguments, `result.append(path)`)
  * integer vs float division, int vs str from `input()`
  * modifying a list or dict while looping over it
  * recursion without a reachable base case
* After the fix: rerun all tests and add a test for this bug.

---

## D4. Last-day checklist

* I can state the time and space complexity of every solution I write.
* I know the templates: hash map, two pointers, sliding window, binary search (first true), BFS, DFS,
  backtracking, topological sort, Dijkstra, union-find, heap top-k, monotonic stack, DP (top-down and bottom-up).
* I know Python's interview toolbox: `Counter`, `defaultdict`, `deque`, `heapq`, `bisect`, `functools.cache`,
  `itertools`, `sorted(key=...)`, slicing, comprehensions, `enumerate`, `zip`.
* I know the Python traps: mutable defaults, aliasing and shallow copies, late binding, `is` vs `==`,
  float precision, floor division with negatives, recursion limit (about 1000; use iteration for deep inputs).
* In the interview: clarify -> examples -> brute force -> optimise -> code -> test with edge cases -> complexity.
  Keep talking, write clean names, and test your code by walking through an example out loud.

---

*End of revision notes.*
