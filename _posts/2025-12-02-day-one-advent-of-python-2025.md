---
layout: post
title: Day One (1) Advent of Python 2025
date: 2025/12/02 06:51:00 +0100
categories:
  - Advent-of-Code
  - Python
  - Programming
---

I've decided to solve advent of code 2025 puzzles in python, and I'll share my thoughts as a series of blogs.

## Puzzle

The Elves have adopted project management, but now they’re too busy to decorate the North Pole—so you've been recruited. To get inside the base and start helping, you must open a safe whose combination is given as a list of dial rotations. The dial shows numbers 0–99, starts at 50, and each instruction moves it left (L) or right (R) by a given number of clicks, wrapping around the circle as needed.

However, your training reveals the safe is a decoy: the real password is the number of times the dial lands on 0 after any rotation. Follow the sequence, count every time the dial points to 0, and that count is the password.

Full link to puzzle: <https://adventofcode.com/2025/day/1>

> I'm using chatgpt to summarize the puzzles.

## My Thoughts

My first thought after reading the puzzle is to use a cycle [linked list](https://en.wikipedia.org/wiki/Linked_list) to represent the dial.

After thinking about if for a while, I decided to use `python`'s default and normal list instead. This is because I've noticed myself over complicating solutions to simple problems, so I try to start simple when I can.

Well, it didn't end well for me.

While I was implementing the function for rotating the dial left, I realized I didn't need a list at all, because the index of the list points to the same number as the list (i.e. `index == dial_numbers[index]`), so I decided to remove the list from the class.

So, now I'm left with a class that is supposed to represent a dial, it has the first number (0), the last number (99), and a pointer (that indicates which number the dial is pointing at) stored. For each rotation, I need to move either left or right, then update the pointer to the new location it is supposed to point at.

Everything looks good until I tried it and I was wrong. It turns out, I didn't take care of the left turn that moves from 0 to 99. My implementation skips 99 completely.

The next issue I had is with numbers larger than 99, the pointer is supposed to point at the same number when you turn the dial 100 times. My initial implementation has it pointing one step ahead.

Both issues I had has to do with not adding or subtracting `1` in an evaluation to satisfy certain edge cases. I think if I had used the linked list, I wouldn't have to deal with this issues.

After getting the answer, I could have rewrote the solution to use a linked list as the representation of the dial, but I decided to dig a deeper hole and see where it leads. The next puzzle builds on this, I wonder if I'll regret not rewriting it later.

## Solution

```python
#! /usr/bin/env python3
"""
Link to puzzle:
https://adventofcode.com/2025/day/1
"""

from pathlib import Path


class Dial:
    """This class represents the dial of the safe.
    It can move both left `cls.l` and right `cls.r`.
    It also keeps track of the current position.
    """

    starting_point = 50
    first_number = 0
    last_number = 99

    def __init__(self):
        """initialization for class."""
        self._pointer = self.starting_point

    def left(self, number: int) -> int:
        """Move left `number` times.
        Parameters:
        - `number`: Number of rotations.
        returns: What the pointer is pointing at after rotation.
        """
        assert number >= self.first_number and number <= self.last_number
        if self._pointer >= number:
            self._pointer = self._pointer - number
        else:
            self._pointer = self.last_number - ((number - self._pointer) - 1)
        assert self._pointer >= self.first_number and self._pointer <= self.last_number
        return self._pointer

    def right(self, number: int) -> int:
        """Move right `number` times.
        Parameters:
        - number: Number of times to move right.
        Returns: Current number the pointer is pointing at.
        """
        assert number >= self.first_number and number <= self.last_number
        if self._pointer + number <= self.last_number:
            self._pointer = self._pointer + number
        else:
            self._pointer = (number - (self.last_number - self._pointer)) - 1
        assert self._pointer >= self.first_number and self._pointer <= self.last_number
        return self._pointer


def run():
    """Entry for code."""
    script_path = Path(__file__).resolve()
    script_dir = script_path.parent
    input_file_path = script_dir / 'day_1_input.txt'
    with open(input_file_path) as file_obj:
        combinations = file_obj.readlines()

    dial = Dial()
    password = 0
    for line in combinations:
        number = int(line[1:])
        if number > Dial.last_number:
            number = number % (Dial.last_number + 1)
        direction = line[:1]
        if direction == 'L':
            pointer = dial.left(number)
        elif direction == 'R':
            pointer = dial.right(number)
        else:
            raise Exception(f'Direction {direction} does not exist.')
        if pointer == 0:
            password += 1

    print(password)


if __name__ == "__main__":
    run()
```
