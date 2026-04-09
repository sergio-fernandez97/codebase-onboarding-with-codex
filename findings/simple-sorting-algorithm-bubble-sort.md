# Simple Sorting Algorithm: Bubble Sort

The simplest sorting example in this repo is the iterative bubble sort implementation in `Python/sorts/bubble_sort.py`.

Why this is a good starting point:
- small and self-contained
- easy control flow
- includes doctests that show expected behavior
- follows the common repo pattern of type hints + docstring examples

Core function:

```python
def bubble_sort_iterative(collection: list[Any]) -> list[Any]:
    length = len(collection)
    for i in reversed(range(length)):
        swapped = False
        for j in range(i):
            if collection[j] > collection[j + 1]:
                swapped = True
                collection[j], collection[j + 1] = collection[j + 1], collection[j]
        if not swapped:
            break
    return collection
```

What it does:
- repeatedly compares adjacent items
- swaps them if they are out of order
- stops early if a full pass makes no swaps

Reference:
- `Python/sorts/bubble_sort.py`
