---
layout: post
title: Day Two (2) Advent of Python 2025
date: 2025/12/03 8:47:00 +0100
categoried: ["Advent-of-Python", "Python", "Programming"]
---

Day 2 thoughts and solutions for advent of code 2025.

## Puzzle

The player must identify and calculate the sum of all "invalid" product IDs within a given list of numerical ranges. An ID is considered invalid if it is formed by a sequence of digits repeated exactly twice (e.g., 55, 6464, 123123) and has no leading zeros.

Link to puzzle: <https://adventofcode.com/2025/day/2>

## My Thoughts

I think I'll use a generator to loop through all the range of ids, and `yield` an invalid id when I find it. I can detect invalid ids by converting the numbers to strings, then comparing the first half of the string with the second half.

The implementation was quite straight forwards, no hiccups.

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
