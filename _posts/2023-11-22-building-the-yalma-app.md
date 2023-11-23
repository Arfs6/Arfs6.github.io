---
layout: post
title: Building The YALMA App
date: 2023/11/22 16:58:00 +0100
category: python
excerpt: 
---
The goal of this blog post is to guide you to build an app in python. Some people get scared when they hear "app", don't worry, I don't think the app will pass 100 lines.

## Introducing YALMA

YALMA (Yet Another Link Manager App) is a link manager build with python. Check this page out for an example of how it looks like; <https://gist.github.com/Arfs6/60e0539ab49d83e12c5bf6e7c401fefb>. The main aim of the app is to accept and store links. For example, you can store the above link in the app and give it the name "YALMA Example". Then when next you need it, you can just open YALMA and ask for it.

## Resources

You might need some resources to be able to do some steps. I don't think me writing it will be a good idea, because of time, and there are lots of excellent resources out there. So, what I am planning to do is to get links to those resources and add it to each step.

## Steps

All the solution to the steps should be in one python file.

### Step 1 - Welcome your user

A nice welcome message to your user is a plus always. Welcome your user and explain briefly what YALMA is:

1. Display `YALMA` followed by a new line. Use *tab* character to shift it a little to the right.
2. Display a brief explanation of what **YALMA** is: `A link manager.`

#### Example

> This is what you should get when you run your code.

```
	YALMA
A link manager.
```

> Tip: A tab character is represented by `\t` in python, It should be in a string.

### Step 2 - Create link

Let's write the code to create a link:

1. Create a function `create_link`.
2. It should prompt the user for a name for the link.
3. It should prompt the user for the link to store.
4. Store both the name and the link provided above in a dictionary. The key should be `name` and `url` for the name and link respectively.
5. Return the created dictionary.
6. For testing purposes, call the function and print what the function returns. *This will be removed later*.

#### Example

```
	YALMA
A link manager.
What is the name of the link? Abdulqadir Ahmad's website
What is the URL (link) of the link? https://arfs6.me
{'name': "Abdulqadir Ahmad's website", 'url': 'https://arfs6.me'}
```

## Have Feedback / Questions?

If you no where to get me, **do not hesitate** to contact me. If you don't, there are useful links at the bottom of this page.
