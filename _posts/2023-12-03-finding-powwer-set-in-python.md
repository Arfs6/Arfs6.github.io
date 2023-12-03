---
layout: post
title: Finding the power set of a set using python
date: 2023/12/03 17:21:00 +0100
category: python
excerpt: My friend and I were solving some math questions and we had to find the power set of a set with 14 elements
---
My friend and I were solving some math questions and we had to find the power set of a set with 14 elements. According to [wikipedia](https://en.wikipedia.org/wiki/Power_set), the power set of a set S is the set of all subsets of S, including the empty set and S itself.

Now, to find the number of elements (I.E. subsets) in the power set, we find 2 to the nth power, where n is the number of elements in the main set. Since our set has 14 elements, she decided to calculate 2 to the nth power manually. It took her a reasonable amount of time to calculate just the number of elements, which is 16384.

At that point, I knew this is no work for a human, and my brain began to figure out how to write it in python. This blog post is me sharing my solution with you.

## The Solution

While I was learning set, chat GPT told me something about using bits to find all the possible subsets of a set. At the time, it flew over my head, but after my brain decided to solve this problem, it remembered it. I think it will be better explaining it with an example.

### Example

Given a set {1, 2, 3}, let's find the power set. The number of elements in our power set is going to be 8.

| Binary | Decimal | Elements   |
|--------|---------|------------|
| 001    | 1       | {3}        |
| 010    | 2       | {2}        |
| 011    | 3       | {2, 3}     |
| 100    | 4       | {1}        |
| 101    | 5       | {1, 3}     |
| 110    | 6       | {1, 2}     |
| 111    | 7       | {1, 2, 3}  |

From the definition given above, it's only the empty set that hasn't been added. Adding it will result to a total of 8 elements. Although the order of the elements aren't "sequential", all the elements have been included.

### Explanation

We start by finding the number of elements in the power set, which in our case is 8.

Next, we write down 1 to 1 - *number of elements in power set* in binary.

Then add zeros to the beginning of all your binary digits (bits) so that they will have equal number of bits. In our case, the largest number had three bits, so we added bits at the beginning of all the other numbers to make it three bits.

For each number, represent each element of your main set with a position in your binary numbers. If the bit corresponding to the number is on (1), add the element to your subset. In our case, 1 was represented by the first bit, 2 by the second bit and 3 by the third bit. For example, our first binary number is *001*. Only the third bit is on, so we only added *3*.

From here, the only missing element in your power set is the empty set. So, add it!

Now, let's figure out how to do this in

## python.

The parts worth mentioning in the python script are [bit wise operators](https://www.geeksforgeeks.org/python-bitwise-operators/) and [generators](https://www.geeksforgeeks.org/generators-in-python/).

I used two bit manipulation operators, `&` and `>>`.

- `&` [`bitwise and`]: I used this to check if the last bit is enabled. By matching it with 1, which has all bit off except the last bit, I'll get 1 only when the last bit is on.
- `>>` [`bitwise right shift`]: I used this to remove the bit I inspected using `&`.

As for the generators, I used it to get all the position of the enabled bits in the current number.

Enough english,

### here is the python code:

```python
#! /usr/bin/env python
# -*- coding: utf-8 -*-


def _getPositions(num):
    """A generator that returns the position of all enabled bits."""
    if num == 0:
        return
    idx = 0
    while num:
        if num & 1:
            yield idx
        num = num >> 1
        idx += 1


def getPowerSet(mainSet):
    """Find the power set of @mainSet
    parameters:
    - mainSet: A list containing all the elements of the set to find it's power set
    Returns:
    - None: Invalid argument
    - list: A list containing all the possible subsets of @mainSet. The subsets are sets.
    """
    if not isinstance(mainSet, list):
        return
    powerSet = []
    max = 2** len(mainSet)
    powerSet.append(set())  # Empty set
    for num in range(1, max):
        subSet = set()
        for idx in _getPositions(num):
            subSet.add(mainSet[idx])
        powerSet.append(subSet)
    return powerSet


def run():
    """Begin code execution"""
    print("Hi. I am here to find the power set of set for you.")
    rawSet = input("Type the elements of your set, separated by comma (,): ")
    if not rawSet:
        print("No set supplied, exiting...")
        return
    mainSet = [int(num.strip()) for num in rawSet.split(",")]
    powerSet = getPowerSet(mainSet)
    print(powerSet)
    print("Total number of sets:", len(powerSet))


if __name__ == '__main__':
    run()
```

## Finding the power set

After finishing the code, we ran it and passed the set with 14 values. It took some seconds before all the output was displayed, and it was over 2000 lines. Should I show you? Okay, I have uploaded the output to a gist, and here is the link: <https://gist.github.com/Arfs6/1efafc44fa97f0ec6ecfb7697ba37504>
