---
layout: post
title: Joining two absolute paths in python
excerpt: ">>> os.path.join('/home/arfs6', '/proj')  # Expecting /home/arfs6/proj"
category: python
tags: python, os-module
date: 2023/10/21 19:55:00 +0100
---
Let's join two absolute paths using the `os` module of python:  

```python
>>> import os
>>> os.path.join('/home/arfs6', '/proj')  # Expecting /home/arfs6/proj
'/proj'
>>>
```

This was unexpected to me. I tried solving it by converting the second path to a relative path, and here is what i got:  

```python
>>> os.path.relpath('/proj')
'../../../proj'
>>> 
```

Looks like python is been too smart here. Just do what I asked you, nothing more, nothing less!  

At this point, I don't know what to do. I don't want to resolve to string manipulation for paths.
