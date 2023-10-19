---
layout: post
title: Did you know? ufw is a python script.
date: 2023:10:19 20:33:00 +0100
excerpt: I wonder which tool I am using that also runs on python.
category: python
tags: python, ufw
---
Out of curiosity, I wanted to know what ufw (uncomplicated Firewall) was made up of. So, I looked for it: 

```bash
$ which ufw
/usr/sbin/ufw
```

Yours might be somewhere else. I then paid the directory a visit and checked what the file was made up of:  

```bash
$ cd /usr/sbin
$ file ufw
ufw: Python script, ASCII text executable
```

I then opened it with vim, but since I can open it here, let me show you some part of it:  

```bash
$ head ufw
#! /usr/bin/python3
#
# ufw: front-end for Linux firewalling (cli)
#
# Copyright 2008-2021 Canonical Ltd.
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU General Public License version 3,
#    as published by the Free Software Foundation.
#
$ grep 'import' ufw
from __future__ import print_function
import os
import sys
import warnings
import ufw.frontend
from ufw.common import UFWError
from ufw.util import error, warn, msg, _findpath, create_lock, release_lock
import gettext
abuahmad in sbin  3:41 PM on Thursday 
$ 
```

So, it turns out, ufw is "just" a python script bundled with a package that lives somewhere in `sys.path`.  

## Conclusion  

So, I wonder, which other tools I use regularly are also python scripts?  
