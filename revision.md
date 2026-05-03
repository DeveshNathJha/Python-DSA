# Part 0: Math Basics for DSA in Python

### 1. Essential Operators & Functions

| Operator / Function | Description | Complexity |
| :--- | :--- | :--- |
| `a // b` | **Floor Division**: Integer result deta hai (lower bound). | $O(1)$ |
| `a % b` | **Modulo**: Remainder nikalne ke liye. | $O(1)$ |
| `pow(a, b, m)` | **Modular Exponentiation**: $(a^b) \pmod m$ fast nikalne ke liye. | $O(\log b)$ |
| `math.gcd(a, b)` | **HCF/GCD**: Greatest Common Divisor calculator. | $O(\log(\min(a, b)))$ |
| `math.isqrt(n)` | **Integer Square Root**: Perfect integer result binary search use karke. | $O(1)$ |

---

### 2. Logic Building: How to Think?

*   **Handling Large Numbers:** Python inherently large numbers handle kar leta hai, lekin interviews mein `ans % (10**9 + 7)` use karna zaroori hota hai overflows simulate karne ke liye.
*   **Division Pitfall:** `5 / 2` ➜ `2.5`. Hamesha `5 // 2` use karo agar indexing chahiye.
*   **Rounding Functions:**
    *   **math.floor(x):** Hamesha piche (number line par left side) jata hai. 2.9 ho ya 2.1, result 2 hi aayega. Negative mein -2.1 ka -3 ho jayega.
    *   **math.ceil(x):** Hamesha aage (number line par right side) jata hai. 2.1 ka bhi 3 kar dega.
    *   **math.trunc(x):** Ye sirf decimal part ko kaat deta hai. Positive numbers ke liye ye floor jaisa dikhta hai aur negative ke liye ceil jaisa.

**Interview Logic:** DSA problems jaise "String to Integer (atoi)" ya "Divide Two Integers" mein humein aksar result ko zero ki taraf round karna hota hai. Wahan `round()` dhokha de sakta hai (Python uses "round to even"), isliye `math.trunc()` ya simple `int()` conversion zyada safe hota hai.

---

### 3. Optimized Primality Test (Answer to Guiding Question)
Agar check karna hai ki `n` prime hai ya nahi, toh humein `1` se `n` tak check karne ki zaroorat nahi hai.

**Logic:** Agar $n = a \times b$, toh kam se kam ek factor $\sqrt{n}$ se chhota ya barabar hoga.
*   **Optimization:** Loop ko sirf `2` se `sqrt(n)` tak chalayein.
*   **Complexity:** Improves from $O(n)$ to **$O(\sqrt{n})$**.

```python
def is_prime(n):
    if n < 2: return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0: return False
    return True
```

---

### 4. Important Formulas & Library Hacks
*   **LCM Formula:** $LCM(a, b) = \frac{a \times b}{GCD(a, b)}$
    *   Python Code: `(a * b) // math.gcd(a, b)`
*   **Modular Arithmetic Rules:**
    1.  $(A + B) \% M = (A \% M + B \% M) \% M$
    2.  $(A \times B) \% M = (A \% M \times B \% M) \% M$
*   **Library Tools:** Use `import math` for `math.comb(n, k)` (nCr) and `math.factorial(n)`.

---

# Part 1: Pythonic "Jugaad" & Built-ins (Quick Revision)

### 1. The "Pythonic" Way (Coding Tips)

| Feature | Syntax | What it does? |
| :--- | :--- | :--- |
| **Swap** | `a, b = b, a` | Bina third variable ke swap. |
| **Enumerate** | `for i, x in enumerate(arr):` | Index aur Value dono saath mein milte hain. |
| **List Comprehension**| `[x**2 for x in arr if x%2==0]` | One-liner loop + condition. |
| **Type Check** | `isinstance(x, (int, float))` | Safe way to check if `x` is a number. |
| **Counter** | `from collections import Counter` | Puray array ki frequency ek second mein nikal leta hai. |

---

### 2. String & Dictionary Hacks

**Strings:**
*   **`s.split()`**: String ko tod kar list bana deta hai (Default: Space).
*   **`" ".join(list)`**: List ko jod kar string bana deta hai.
*   **`s.strip()`**: Aage aur peeche ke faltu spaces saaf kar deta hai.
*   **`s[::-1]`**: String reverse karne ka sabse fast tareeka.

**Dictionaries:**
*   **`d.get(key, 0)`**: Agar key nahi mili toh error dene ke bajaye `0` dega.
*   **`d.items()`**: Key aur Value dono ke upar loop chalane ke liye.
*   **Dict Comprehension**: `{k: v for k, v in d.items() if v > 1}` (Duplicates nikalne ke liye best).

---

### 3. Loop Power: `for...else`
Python mein `for` loop ke saath `else` bhi lag sakta hai.
*   **Logic:** `else` wala block tabhi chalta hai jab loop **poora bina kisi `break` ke** khatam ho jaye.
*   **Interview Use:** Prime checking ya search algorithms mein kaam aata hai.

```python
for i in range(2, n):
    if n % i == 0:
        print("Not Prime")
        break
else:
    print("Prime") # Loop pura chala, breaks nahi hua!
```

---

# Part 2: DSA Patterns & Logic (Advanced)

### 1. Lists (Arrays)

| Operation | Syntax | Time Complexity | Note |
| :--- | :--- | :--- | :--- |
| **Access** | `arr[i]` | $O(1)$ | Direct memory access via index. |
| **Append** | `arr.append(val)` | $O(1)^*$ | Amortized constant time. |
| **Insert** | `arr.insert(i, val)` | $O(n)$ | Requires shifting elements to the right. |
| **Delete (End)** | `arr.pop()` | $O(1)$ | Removing from the end is fast. |
| **Delete (Index)**| `arr.pop(i)` / `del` | $O(n)$ | Requires shifting elements to the left. |
| **Search** | `val in arr` | $O(n)$ | Linear scan. |
| **Slicing** | `arr[a:b]` | $O(k)$ | $k$ is slice length. |

---

### 2. Slicing Mastery

Python slicing pattern: `[start : stop : step]`

*   **Reverse**: `arr[::-1]`
*   **Last k elements**: `arr[-k:]`
*   **Skip elements**: `arr[::2]` (Every second element)
*   **Copy**: `arr[:]` (Creates a shallow copy)

---

### 3. Logic Building: How to Think?

When solving Array problems, use these mental models:

1.  **Complexity Check**: If you see a nested loop ($O(n^2)$), think:
    *   **Can I Sort first?** ($O(n \log n)$)
    *   **Can I use a Hash Map/Set?** ($O(n)$ space for $O(n)$ time)
    *   **Can I use Two Pointers or a Sliding Window?**
2.  **Pattern Recognition**: 
    *   "Contiguous subarrays" -> **Sliding Window**.
    *   "Sorted array" -> **Binary Search** or **Two Pointers**.

---

### 4. Advanced Sliding Window (Variable Size)
Fixed window (`sum(arr[:k])`) toh easy hai, par variable window (jab window size fix nahi hoti) zyada important hai.

**Pattern: Shrinking Window (While loop)**
Jab condition match na kare (jaise duplicate mil jaye), toh `left` pointer ko tab tak move karo jab tak condition thik na ho jaye.

```python
def variable_window(s):
    seen = set()
    left = 0
    max_len = 0
    for right in range(len(s)):
        while s[right] in seen: # Condition Fail!
            seen.remove(s[left]) # Shrink from left
            left += 1
        seen.add(s[right]) # Expand from right
        max_len = max(max_len, right - left + 1)
    return max_len
```

---

### 5. Array Magic (Math & Bitwise)

*   **Arithmetic Progression (AP) Sum**: Agar range 1 se start nahi hoti toh use:
    *   `Sum = (n / 2) * (First + Last)`
*   **XOR Trick**: Missing number nikalne ke liye XOR use karo.
    *   `xor_all ^= i`. Saare expected numbers aur given numbers ko XOR kar do, jo bacha woh missing hai!

---

### 6. Try-Except: Safe Coding
Interviews mein kabhi-kabhi data malformed ho sakta hai (e.g., string in int list). 
```python
try:
    val = int(user_input)
except Exception as e:
    print(f"Error pakda gaya: {e}")
```

---

### 7. Deque vs List
| Feature | `list.pop(0)` | `deque.popleft()` |
| :--- | :--- | :--- |
| **Complexity** | $O(n)$ | **$O(1)$** |
| **Mechanism** | Shifts elements left ⬅️ | Direct pointer manipulation 📍 |
| **Best Use Case** | Random index access | Queues, BFS, Sliding Window |