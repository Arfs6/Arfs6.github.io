---
layout: post
title: Day Three (3) - Advent of Python 2025
date: 2025/12/26 17:41:00 +0100
categories: ["Advent-of-Python", "Python", "Programming"]
---

## Puzzle

This puzzle is about scanning rows of digits (called battery banks) and, for each row, choosing exactly two digits in their original order to form the largest possible two-digit number. You do this independently for every row, then add up all those maximum two-digit numbers to get the final result.

Link to puzzle: <https://adventofcode.com/2025/day/3>

## My Thoughts

I felt really good after writing the solution for the first part. I started with a sudo code this time.

The part of my solution that gets the largest possibel two digit number works this way:

It gets the largest digit in the list (bank of batteries) starting from the beginning till the second to the last number. That will be the first digit of the two digit number.

It then loops through the list again, but this time it starts from the next number after the first digit, till the end of the list. The largest number in this section is the second digit.

I used a generator to sum my results this.

My first solution was almost perfect, I just had to fix one list index problem.

## Solution

```python
#! /usr/bin/env python3
"""
Solution for advent of code puzzle for day 3
link: https://adventofcode.com/2025/day/3
"""

from __future__ import annotations
from pathlib import Path


def get_maximum_joltage(bank: list[str]) -> str:
    """Return the maximum joltage that can be gotten from the given bank of batteries."""
    first_digit = '0'
    first_digit_idx = '0'
    for idx, battery in enumerate(bank[:-1]):
        if battery > first_digit:
            first_digit = battery
            first_digit_idx = idx
    second_digit = '0'
    for battery in bank[first_digit_idx + 1:]:
        if battery > second_digit:
            second_digit = battery
    return first_digit + second_digit


def solution(banks):
    """Solution of the puzzle."""
    for rating in banks:
        bank = list(rating)
        yield int(get_maximum_joltage(bank))


def run():
    """Entry point of the script."""
    input_path = Path(__file__).parent.resolve() / 'day_3_input.txt'
    with open(input_path) as file_obj:
        lines = file_obj.readlines()
        banks = [line[:-1] for line in lines]  # truncate the '\n' character.
        print(sum(solution(banks)))


if __name__ == '__main__':
    run()
```

## Part 2

Instead of picking two batteries from each bank, you must now pick exactly twelve, keeping their original order. The digits you choose form a 12-digit number, and your goal is to make that number as large as possible for each bank. As before, you do this independently for every line of input, then sum all of the maximum 12-digit joltages to get the final answer.

## My Thoughts

My first idea was to make the function that gets the largest two digit number recursive. The condition for the recursion is the number of digits required.

The input for the function is a list of digits and a number. The list represents the bank of batteries, while the number represents the number of digits in the largest possible number that should be gotten from the list.

The recursion stops when the number of digit reaches zero.

For each call of the function, it looks for the largest number starting from the beginning of the list till a point where the rest of the digits can be found. For instance, if we have a list `[2, 3, 1]` and the number is 1, the function will search through the first two items.

Lastly, the function returns the current largest digit plus a recursive call to the same function with the list starting from the next number after the current largest digit and the number decreased by 1.

## Solution

```python
#! /usr/bin/env python3
"""
Solution for advent of code puzzle for day 3
link: https://adventofcode.com/2025/day/3
"""

from __future__ import annotations
from pathlib import Path


def get_maximum_joltage(bank: list[str], digits: int) -> str:
    """Return the maximum joltage that can be gotten from the given bank of batteries."""
    if digits <= 0:
        return ''
    digit = '0'
    digit_idx = 0
    for idx, battery in enumerate(bank[: len(bank) - (digits - 1)]):
        if battery > digit:
            digit = battery
            digit_idx = idx
    return digit + get_maximum_joltage(bank[digit_idx + 1 :], digits - 1)


def solution(banks):
    """Solution of the puzzle."""
    for rating in banks:
        bank = list(rating)
        yield int(get_maximum_joltage(bank, 12))


def run():
    """Entry point of the script."""
    input_path = Path(__file__).parent.resolve() / 'day_3_input.txt'
    with open(input_path) as file_obj:
        lines = file_obj.readlines()
        banks = [line[:-1] for line in lines]  # truncate the '\n' character.
        print(sum(solution(banks)))


if __name__ == '__main__':
    run()
```
