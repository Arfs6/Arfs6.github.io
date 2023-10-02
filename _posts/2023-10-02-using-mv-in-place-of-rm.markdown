---
layout: post
title: Using mv instead of rm
category: linux
tags: linux
excerpt: The `rm` command is dangerous. I have created an 
date: 2023/10/02 11:35:00 +0100
---
The `rm` command is dangerous. I have created an alias to use `2smvrm` instead of it. The command is in my `~/.bashrc`.  

```bash
alias rm='mv --force -t ~/.local/share/trash '
```

The `-t` option allows me to specify the target directory at the beginning of the command. The alias moves all the files specified to `~/.local/share/trash`. This means, if I change my mind at any time, I can pay the directory a visit.  

If I really want to use `rm`, I use `/bin/rm`.  

There are a lot of issues with the above command.  

1. If a file with the same name with the one I want to move has already exist, it will fail.  
2. The files might use a lot of space overtime. I thought of using the `/tmp/` directory since the os deletes file in there automatically.  
