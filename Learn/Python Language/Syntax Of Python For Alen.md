## ✅ Basic Syntax


|Concept|Syntax / Example|Description|
|---|---|---|
|Variable|`x = 10`|Assign value|
|Print|`print("Hello")`|Display output|
|Comment|`# Comment`|Single-line comment|
|Multi-line|`""" comment """`|Multi-line string or comment|
|Input|`input("Enter: ")`|Take string input|
|Type casting|`int("5")`, `str(10)`|Convert types|
|f-Strings|`f"Name: {x}"`|Format strings with variables|

---

## ✅ Data Types

|Type|Example|Description|
|---|---|---|
|`int`|`10`, `-3`|Whole number|
|`float`|`3.14`, `-0.5`|Decimal number|
|`bool`|`True`, `False`|Boolean values|
|`str`|`"hello"`, `'a'`|Text strings|
|`list`|`[1, 2, 3]`|Ordered, mutable collection|
|`tuple`|`(1, 2)`|Ordered, immutable|
|`set`|`{1, 2, 3}`|Unordered, unique values|
|`dict`|`{"a": 1, "b": 2}`|Key-value pairs|

---

## ✅ Operators

| Type       | Operators                | Description                   |
| ---------- | ------------------------ | ----------------------------- |
| Arithmetic | `+ - * / // % **`        | Basic math                    |
| Assignment | = += -= *= /= //= **= %= | Modify and assign             |
| Comparison | == != > < >= <=          | Compare values                |
| Logical    | `and or not`             | Combine conditions            |
| Bitwise    | `&                       | ^ ~ << >>`                    |
| Membership | `in`, `not in`           | Check if value is in sequence |
| Identity   | `is`, `is not`           | Compare object identity       |

---

## ✅ Conditionals

|Syntax|Description|
|---|---|
|`if condition:`|If block|
|`elif another_condition:`|Else-if block|
|`else:`|Else block|

---

## ✅ Loops

|Syntax|Description|
|---|---|
|`for i in range(5):`|Loop 0 to 4|
|`while condition:`|While loop|
|`break`|Exit loop early|
|`continue`|Skip to next iteration|
|`pass`|Do nothing (placeholder)|

---

## ✅ Functions

|Syntax|Description|
|---|---|
|`def func():`|Define function|
|`return value`|Return from function|
|`lambda x: x + 1`|Anonymous function|
|`*args`, `**kwargs`|Variable arguments|

---

## ✅ String Methods

|Method|Description|
|---|---|
|`str.lower()`|Lowercase|
|`str.upper()`|Uppercase|
|`str.title()`|Capitalize first letters|
|`str.strip()`|Trim whitespace|
|`str.replace(a, b)`|Replace substring|
|`str.find(x)`|Index of x or -1|
|`str.count(x)`|Count occurrences|
|`str.startswith(x)`|True if starts with x|
|`str.endswith(x)`|True if ends with x|
|`str.split()`|Split string into list|
|`' '.join(list)`|Join list into string|
|`str.isdigit()`|Check if all characters are digits|
|`str.isalpha()`|Check if all are letters|
|`str.isalnum()`|Letters or digits|

---

## ✅ List Methods

|Method|Description|
|---|---|
|`list.append(x)`|Add to end|
|`list.insert(i, x)`|Insert at index|
|`list.pop(i)`|Remove at index (or last)|
|`list.remove(x)`|Remove first occurrence|
|`list.clear()`|Empty list|
|`list.index(x)`|Index of value|
|`list.count(x)`|Count value|
|`list.sort()`|Sort in-place|
|`list.reverse()`|Reverse in-place|
|`sorted(list)`|Return sorted copy|
|`list.copy()`|Shallow copy|
|`list.extend(list2)`|Add all from another list|

---

## ✅ Dictionary Methods

|Method|Description|
|---|---|
|`dict.get(key)`|Get value or None|
|`dict[key] = value`|Set value|
|`dict.pop(key)`|Remove key and return value|
|`dict.update(dict2)`|Merge dictionaries|
|`dict.clear()`|Remove all entries|
|`dict.keys()`|Get all keys|
|`dict.values()`|Get all values|
|`dict.items()`|Key-value pairs|

---

## ✅ Set Methods

|Method|Description|
|---|---|
|`set.add(x)`|Add item|
|`set.remove(x)`|Remove item or error|
|`set.discard(x)`|Remove item safely|
|`set.pop()`|Remove random element|
|`set.clear()`|Remove all elements|
|`set.union(s2)` or `|`|
|`set.intersection(s2)` or `&`|Common elements|
|`set.difference(s2)` or `-`|Elements in one not other|
|`set.symmetric_difference(s2)` or `^`|In one but not both|

---

## ✅ File Handling

|Syntax|Description|
|---|---|
|`open(filename, mode)`|Open file|
|`f.read()`|Read whole file|
|`f.readline()`|Read one line|
|`f.readlines()`|Read all lines as list|
|`f.write("text")`|Write text|
|`f.close()`|Close file|
|`with open(...) as f:`|Context manager (auto close)|

---

## ✅ Built-in Functions

|Function|Description|
|---|---|
|`len()`|Length of object|
|`type()`|Get type|
|`range()`|Generate sequence|
|`enumerate()`|Get index and value|
|`zip()`|Combine iterables|
|`reversed()`|Reverse iterable|
|`sorted()`|Sort iterable|
|`sum()`|Sum numbers in list|
|`min()`, `max()`|Get min/max values|
|`abs()`|Absolute value|
|`round()`|Round number|
|`divmod(a, b)`|Get quotient and remainder|
|`map(func, iterable)`|Apply function to all items|
|`filter(func, iterable)`|Filter items|
## ✅ 2D Array (Matrix) Operations in Python

#### 🧩 Declare & Access

matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]  
value = matrix[0][2] # Access element (1st row, 3rd col) → 3  
matrix[1][1] = 99 # Update value

#### 🔁 Loop Through 2D Array

```python
for row in matrix:  
  for val in row:  
    print(val, end=" ")
```

---

## ✅ Extra String Methods (Useful Ones)

|Method|Description|Example|
|---|---|---|
|str.zfill(5)|Pad with zeros on the left|"42".zfill(5) → "00042"|
|str.center(w, ch)|Center string in width `w` using `ch`|"hi".center(6, "-") → "--hi--"|
|str.ljust(n), rjust(n)|Left or right justify with spaces|"ok".rjust(5) → " ok"|
|str.partition(x)|Split into 3 parts around x|"abc:def".partition(":")|
|str.swapcase()|Swap upper and lower case|"AbC".swapcase() → "aBc"|
|str.casefold()|Stronger lower() for comparisons|"straße".casefold() → "strasse"|

---

## ✅ List Tricks You Might’ve Missed

|Method/Usage|Description|Example|
|---|---|---|
|[0] * n|Create list with `n` zeros|[0] * 5 → [0, 0, 0, 0, 0]|
|list(range(n))|List from 0 to n-1|range(5) → [0, 1, 2, 3, 4]|
|[x for x in list]|List comprehension|[x*x for x in range(3)] → [0, 1, 4]|
|zip(a, b)|Combine two lists|zip([1,2], [3,4]) → (1,3), (2,4)|
|reversed(list)|Reverse iterator|list(reversed([1,2,3])) → [3,2,1]|

---

## ✅ Python Input/Output for 2D Array

#### 📥 Input Example (single-line row-wise)

```python
matrix = [list(map(int, input().split())) for _ in range(3)]
```

or

```python
matrix = []
for _ in range(3):
    row = list(map(int, input().split()))
    matrix.append(row)
```

```
Input: 1 2 3 ↵ 4 5 6 ↵ 7 8 9
```

#### 📤 Output Example

```python
for row in matrix:  
  print(" ".join(map(str, row)))
```