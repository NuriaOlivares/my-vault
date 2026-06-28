# Python Notes

> Summary: Python syntax, patterns and concepts I am learning. Updated as I go.

I know programming concepts well. What I need here is the Python-specific way to do things.

---

## Type hints (equivalent to TypeScript types)

```python
# TypeScript: function greet(name: string): string
def greet(name: str) -> str:
    return f"Hello, {name}"

# TypeScript: function add(a: number, b: number): number  
def add(a: int, b: int) -> int:
    return a + b

# Optional (like TypeScript's string | null)
from typing import Optional
def find_user(id: int) -> Optional[str]:
    return None  # or a string
```

---

## List operations (equivalent to JS array methods)

```python
numbers = [1, 2, 3, 4, 5]

# JS: numbers.map(n => n * 2)
doubled = [n * 2 for n in numbers]

# JS: numbers.filter(n => n > 2)
big = [n for n in numbers if n > 2]

# JS: numbers.find(n => n > 2)
first_big = next((n for n in numbers if n > 2), None)
```

These are called "list comprehensions" — very common in Python.

---

## Dictionary (equivalent to JS object / TypeScript Record)

```python
user = {"name": "Ana", "age": 30}

# Access
user["name"]        # like user.name or user["name"] in JS
user.get("email")   # safe access, returns None if missing (like user?.email)

# Add / update
user["email"] = "ana@example.com"
```

---

## F-strings (equivalent to JS template literals)

```python
name = "Ana"
# JS: `Hello, ${name}`
message = f"Hello, {name}"
```

---

## Things I always forget

- Python uses indentation to define blocks, not curly braces.
- `None` is Python's `null`.
- `True` and `False` are capitalised (not lowercase like JS).
- `len(list)` not `list.length`.
- Use `==` for equality, never `===` (Python does not have triple equals).

---

## Still learning

- How to structure a Python project (packages, modules, imports).
- Virtual environments — venv vs conda vs uv.
- How async/await works in Python (asyncio).
- Pydantic for data validation (seems like Zod for Python).