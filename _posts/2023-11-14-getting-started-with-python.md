---
layout: post
title: Getting started with python
date: 2023/11/14 14:14:00 +0100
category: python
excerpt: My goal in this article is to get you to write some python code. I am a big believer in learning by doing
---
My goal in this article is to get you to write some python code. I am a big believer in learning by doing, and this article is written with that in mind.  

## Project

The goal is to create a score resolver. It should request the user to enter his / her score and tell the user what grade he / she has.


## Requirements  

You can write your python code anywhere, but you need the python interpreter to be able to run the code. The python interpreter reads your code and instructs the computer on what to do.

The app I'll suggest is pydroid. It is available on Google playstore, I'm not sure of Apple app store.  

Pydroid has an interface for writing code, running code and even an interactive code execution with python.

## Python repl  

When you click interpreter in pydroid, you're getting the python repl. It has three greater than sign (`>>>`) then a cursor. The greater than sign is called a prompt. When you type in a command and hit enter, the interpreter executes your command and returns the result. Then it displays a new prompt, waiting for your next command.  

## Steps  

Computers are stupid by design. So, in order to instruct it, you need to tell it everything in details. You can't just say "Go and get me a coffee". You'll have to tell it how to do it and when to do it. e.g.  

- Stand up immediately.
- Walk straight 10 feets.  
- Get a cup from ...  

You get my point? Now, our goal is to write a program that figures out what grade a score is. Let's write down our instructions in english and then figure out how to replicate it in python.  

1. Ask the user for his / her score.
2. Store what the user wrote.
3. Fine the grade corresponding to his / her score.
4. Display the corresponding grade.

As you can see, almost all the steps are detailed, except step 3. We need to tell the stupid computer how to get a grade from a score.

How about we use greater than and less than? E.G. When the score is less than 30, we know it is an F.

Expanding step 3, we'll have:  

Let the number the user entered be `score`.

- If `score` is greater than or equal to 0 and it is less than 30, we display *F*.
- If `score` is greater than or equal to 30 and it is less than 40, we display *E*.
- If `score` is greater than or equal to 40 and it is less than 50, we display *D*.
- If `score` is greater than or equal to 50 and it is less than 60, we display *C*.
- If `score` is greater than or equal to 60 and it is less than 70, we display *B*.
- If `score` is greater than or equal to 70 and it is less than or equal to 100, we display *A*.

Let's get started!  

## Displaying output  

You might be wondering, according to the steps detailed above, we should be starting with accepting input. Yes, you're right. I decided to start with the last item in our list because it has the less concepts.  

### Hello Python World!

Open pydroid. At the top right, there is a button with three dashes. Click it and click interpreter. You will see something like this:

```python
>>> |
```

Where `|` represents your cursor.

Now, type `print("Hello Python World!")`. Now, the interpreter will look like this:

```python
>>> print("Hello Python World!")
```

You have just typed an instruction that python will interpret and tell the computer what to do. Now, hit enter to execute it. You'll have something like this now:

```python
>>> print("Hello Python World!")
Hello Python World!
>>>
```

> If your output doesn't look like mine, or if you get an error, compare your code with mine. Scrutinize it, character by character.

### Explanation

We can break the above code into two:

- `print()`
- `"Hello Python World!"`

The first one is a callable object. Everything in python is an object (My laptop is an object), and each object has it's own property (My laptop has a typing property. Which means, I can type using it). When you call a callable object, it does something for you and returns another thing. You can also give a value to a callable to work with.

To call a callable, you write the name of the callable (`print`) followed by a pair of brackets (`(` and `)`). E.G. To call the `print` callable, you type `print()`. Let's try it!

```python
>>> print()

>>>
```

> There is no space between the callable and the pair of brackets.

As you can see, we got an empty line. That is what the print function does when you don't give anything to display.

To give `print` what to display, you write it between the brackets. Let's try it!

```python
>>> print(Hello)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'Hello' is not defined
>>> 
```

> The above text might differ slightly from yours, don't worry as long as the last line is a `NameError`.

We got an error!!! If you compare the first successful print command and this one, you'll see that we didn't use quotation marks in this one.

The problem is, python doesn't know what `Hello` means. It knows `print` is a callable object, but it doesn't know what `Hello` is.

We know, `Hello` is a text, how can we tell pyton? By quoting the text. If you quote the text, python will know it is a text. Let's try it!

```python
>>> print("Hello")
Hello
>>> 
```

Now that you know how to print `Hello World!`, try printing:  

- **Abdulqadir Ahmad**.  
- Your name.  

> If / when you get an error, read the concept again and make sure you're using the right brackets and `print`. `print` is not the same with `Print`. Python is case sensitive.

## Storing data  

> To be continued.
