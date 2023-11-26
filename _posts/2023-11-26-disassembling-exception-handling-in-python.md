---
layout: post
title: Disassembling exception handling in python
date: 2023/11/26 15:00:00 +0100
category: python
excerpt: As a user, I wouldn't want an app to crash just because I supplied the wrong input
---
If you have written some code in python, then you have most probably met an exception. Exceptions occurs when an operation fails. Example, converting *one* to an integer.

When an exception is raised and it isn't handled, python displays an error to the console and exits the program. As a user, I wouldn't want an app to crash just because I supplied the wrong input. This is where exception handling comes.

## Introducing the `try` block

`try` blocks are used to handle exceptions in python. It has three clauses:

1. [`except`](#except)
2. [`else`](#else)
3. [`finally`](finally)

The code in `except` and `else` blocks executes based on what happens in the `try` block and the code in the `finally` block always runs.

Now, let me use an example to explain what each blocks does.

Given the following code:

```python
age = int(input("How old are you? "))
```

What will happen when I type twenty? Let's run it and see what we'll get:

```
How old are you? Twenty
Traceback (most recent call last):
  File "/tmp/main.py", line 1, in <module>
    age = int(input("How old are you? "))
ValueError: invalid literal for int() with base 10: 'Twenty'
```

This isn't something we will want our users to see. A better thing is something like `Have no idea what Twenty is.`.

Now, to be able to handle an exception, we need to put the code that can raise the exception in a `try` block. E.G.

```python
try:
    age = int(input("How old are you? "))
```

Now, let's run this code and see what will happen:

```
  File "/tmp/main.py", line 2
    age = int(input("How old are you? "))
SyntaxError: expected 'except' or 'finally' block
```

A `try` block must  have at least one [`except`](#except) or a [`finally`](#finally) block.

This ties to the next section:

## except {#except}

The most basic form of an `except` statement is `except:`, for example:

```python
try:
    age = int(input("How old are you? "))
except:
    print("I think you didn't type a number. Try again!")
```

Let's try and recreate the error again.

```
I think you didn't type a number. Try again!
```

It worked! And it smells! Let me explain.

The above `except` statement doesn't specify which exception it's handles. This has the effects of passing all unhandled exceptions to it. Which is something you will not like. Why? some exceptions are meant to be handled differently. For example, when you hit ctrl+c while the above code is waiting for user input, python raises a `KeyboardInterupt` exception. This usually signals the user wants to exit the program, so you are supposed to exit the program not print something.

So, how do we specify which exception to handle? by writing it after `except`. How do we know which exception to handle? Usually, I allow python to tell me. If you check the error we got in our first example, the last line is:

```
ValueError: invalid literal for int() with base 10: 'Twenty'
```

The exception to handle in this case is `ValueError`.

Let's handle `ValueError`

```python
try:
    age = int(input("How old are you? "))
except ValueError:
    print("I think you didn't type a number. Try again!")
```

Hmmmm, our code has stopped smelling.

The last info for this section is, you can have more than one `except` blocks under a `try` block. So, you can handle `KeyboardInterupt` too if you like.

## else {#else}

The code in the `else` block depends on the code in the `try` block to run without an exception. In our case, we can do something with the age variable. E.G.

```python
try:
    age = int(input("How old are you? "))
except ValueError:
    print("I think you didn't type a number. Try again!")
else:
    print("Now I know you're", age, "years old.")
```

Now, let's run our code and pass it an appropriate value.

```
How old are you? 20
Now I know you're 20 years old.
```

## finally {#finally}

The `finally` block always executes. In our case, we can print a goodbye to our user.

```python
try:
    age = int(input("How old are you? "))
except ValueError:
    print("I think you didn't type a number. Try again!")
else:
    print("Now I know you're", age, "years old.")
finally:
    print("Thank you for sailing with us.")
```

Let's try with an appropriate input:

```
How old are you? 20
Now I know you're 20 years old.
Thank you for sailing with us.
```

OK... Let's give it *Twenty* now:

```
How old are you? Twenty
I think you didn't type a number. Try again!
Thank you for sailing with us.
```

## Conclusion

This is an introduction to exception handling in python. Lots of things has been ignored intensionally.
