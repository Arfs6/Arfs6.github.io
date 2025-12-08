---
layout: post
title: Day Two (2) - Advent of Python 2025
date: 2025/12/03 8:47:00 +0100
categories: ["Advent-of-Python", "Python", "Programming"]
---

The first part of day 2's solution was straight forward, but I had to rewrite the second part.

## Puzzle

The player must identify and calculate the sum of all "invalid" product IDs within a given list of numerical ranges. An ID is considered invalid if it is formed by a sequence of digits repeated exactly twice (e.g., 55, 6464, 123123) and has no leading zeros.

Link to puzzle: <https://adventofcode.com/2025/day/2>

## My Thoughts

I think I'll use a generator to loop through all the range of ids, and `yield` an invalid id when I find it. I can detect invalid ids by converting the numbers to strings, then comparing the first half of the string with the second half.

The implementation was quite straight forward, no hiccups. I think this was because python handled most o the string manipulation (splitting the text) for me.

## Solution

```python
#! /usr/bin/env python3
"""
Solution for day 2 part 1 puzzle.
link: https://adventofcode.com/2025/day/2
"""

from pathlib import Path


def invalid_ids(ids: str):
    """A generator that yields all invalid ids."""
    list_ids_str = ids.split(',')
    list_ids_int = [(int(num.split('-')[0]), int(num.split('-')[1])) for num in list_ids_str]
    for start, stop in list_ids_int:
        for num in range(start, stop+1):
            num_str = str(num)
            length = len(num_str)
            if length % 2 != 0:
                continue
            if num_str[:length//2] == num_str[length//2:]:
                yield num

def run():
    """Entry point."""
    cwd = Path(__file__).parent
    input_path = cwd / "day_2_input.txt"
    with open(input_path) as file_obj:
        ids = file_obj.read()

    print(sum(invalid_ids(ids)))


if __name__ == "__main__":
    run()
```

## Part 2

The criteria for invalid IDs are updated: an ID is now invalid if it consists of a sequence of digits repeated two or more times (e.g., 12341234, 1212121212, 1111111). Using the same ranges as before, the player must identify all IDs that meet this new rule and calculate their sum.

## My Thoughts

The first thing I did was to delete the lines that compared the first half of the id with the second half and replaced it with a function call to `is_invalid(id)`. The `is_invalid` function is supposed to check if an id is valid and return `True`, otherwise it returns `False`.

I had to rewrite the `is_invalid` function because I was having some weird edge cases, like "111" not been recognized as an invalid id. After deleting the first implementation, I wrote down the problem and a sudo code of the solution, before I implemented it in python. Everything worked out nicely after that.

The `is_invalid` function works by comparing the ID in chunks (parts). The parts starts from one character each, until half of the characters in the ID is selected as a part. If all the parts are equal, the ID is a pattern and it's invalid, so `True` is returned.

I don't know what my problem with list indexes and slices are, I hope I'll figure it out before I finish all the puzzles.

## Solution

```python
#! /usr/bin/env python3
"""
Solution for day 2 part 2 puzzle.
link: https://adventofcode.com/2025/day/2
"""

from pathlib import Path


def Is_invalid(num: int) -> bool:
    """Checks if an id is invalid.
    returns: bool
    """
    num_str = str(num)
    length = len(num_str)
    half = length // 2
    if length <= 1:
        return False
    for stop_idx_first_part in range(1, length):
        if stop_idx_first_part > half and length > 3:
            break
        first_part = num_str[:stop_idx_first_part]
        start_idx_other_parts = range(stop_idx_first_part, length, stop_idx_first_part)
        stop_idx_other_parts = range(stop_idx_first_part * 2, length + 1, stop_idx_first_part)
        for start_idx_other_part, stop_idx_other_part in zip(start_idx_other_parts, stop_idx_other_parts):
            if first_part != num_str[start_idx_other_part: stop_idx_other_part]:
                break
            elif stop_idx_other_part == length:  # We're reach the end and the parts are all equal.
                return True
    return False


def invalid_ids(ids: str):
    """A generator that yields all invalid ids."""
    list_ids_str = ids.split(',')
    list_ids_int = [(int(num.split('-')[0]), int(num.split('-')[1])) for num in list_ids_str]
    for start, stop in list_ids_int:
        for num in range(start, stop+1):
            if Is_invalid(num):
                yield num

def run():
    """Entry point."""
    cwd = Path(__file__).parent
    input_path = cwd / "day_2_input.txt"
    with open(input_path) as file_obj:
        ids = file_obj.read()

    print(sum(invalid_ids(ids)))


if __name__ == "__main__":
    run()
```
