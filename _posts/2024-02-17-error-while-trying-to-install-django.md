---
layout: post
date: 2024/02/17 10:03:00 +0100
title: Error while trying To Install Django
category: python
---
I was trying to install `django` on ubuntu 20.04 on WSL and I was getting an error. The error has to do with `mysqlclient`, and here is the relevant snippet:

```
      Exception: Can not find valid pkg-config name.
      Specify MYSQLCLIENT_CFLAGS and MYSQLCLIENT_LDFLAGS env vars manually
```

I can remember coming across this once, and this time I decided to write a blog on how to solve it.

## Solution

The solution is pretty straight forward - I just needed to install a couple of packages;

```
sudo apt-get install python3-dev default-libmysqlclient-dev build-essential pkg-config
```

I got this from the [README](https://github.com/PyMySQL/mysqlclient/blob/main/README.md) of the `mysqlclient` python package.

The error originated because `pip` needs the `mysqlclient` library in order to build the wheels and it couldn't find it.

> By the way, if you're using a python version that wasn't pre-installed, you should install `python3.X-dev` instead of `python3-dev`; where `X` is the minor version (e.g. `python3.12-dev`).
