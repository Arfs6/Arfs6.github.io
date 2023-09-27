---
layout: post
date: 2023/09/27 13:49:00 +0100
categories: linux
tags: linux
title: Navigating Linux File System
excerpt: When I first layed my hands on a unix computer, I was confused. I had no idea where to keep my files or where some files are located
---
When I first layed my hands on a unix computer, I was confused. I had no idea where to keep my files or where some files are located. Fast forward, now I am comfortable in linux. I spend most of my time in [wsl](https://learn.microsoft.com/en-us/windows/wsl/about). I am even writing this article in it.  

In this post, I will walk you through the linux file system. You'll know where to keep your file and where some key folders are located. But before we start, let's go through some jargons.  

## Jargons  

1. Directory: A directory is like a folder in windows. It holds other directories and files.  
2. */*: Linux uses a forward slash (*/*) to seperate directories and files. Windows uses a back slash (*\*).  
3. path: Specifies location of a file / directory in a filesystem. e.g. `/root/.bashrc`. Remember: `/` is used to seperate files and directories in linux. So, `/root/.bashrc` means the `.bashrc` file is in the `root` directory.  
4. File Permissions: This determines who can read, write or execute a file / directory.  

## Root Directory - `/`  

This is the main directory. it holds all other directories. Typically, in windows, a path to a file will start with `c:`. Where the `c` is the drive letter. In linux, a path always starts with `/`. Windows uses the drive letter to represent a storage device (like flash) or a partition. While on linux, all storage devices and partitions are in the root directory.  

## Home Directory - `~`  

This is usually where you find yourself when you login. If you're login as the root user, that will be `/root/`. If you're login as another user, e.g. ubuntu, that will be `/home/ubuntu/`. A user has read, write and execute permissions to all the files and folders in his home directory unless explicitly changed. `~` is a special character that represents a users home directory. You can use it in paths.  

This is where I keep my files. I have a folder `docs` for documents, `repos` for git repos, `projects` for my projects and `alx` for [alx](https://alxswe.com) related files.  

## Temporary files directory - `/tmp/`  

This is a folder where you can keep temporary files. The operating system delete files that are not used for a while. So, don't keep anything useful here. Some programs keeps there temporary files here. I keep some files I download here. e.g. A script for installing something. I often use it when I want a file temporarily. e.g. A small C program.

## Executables Directory - `bin`  

The `bin` directory is used for holding executables. There are several `bin` directories. Some of the most important include:  

- `/usr/bin/` and `/usr/local/bin/`: Most apps you install using the `apt` command and default programs like `ls` are here.  
- `~/.local/bin/`: This bin directory is local to a user. My [neovim](https://github.com/neovim/neovim) executable is here.  

## Other important Directories  

- `/var/log/`: Some program store it's log files here. Useful for debugging.  
- `/etc/`: System configuration files and other program configuration files are here. Don't mess with files here unless you know what you're doing.  
- `~/<program name>/`: Where `<program name>` is a program's name; Holds user specific configuration for that program. e.g. `~/.ssh/` for ssh and `~/.vim/` for vim.
- `~/.config/`: Config directory for some programs.  

## Conclusion  

With the information you have now, you can navigate arround the linux file system with ease. With time, you'll recognize other patterns and key directories like `lib` and `/var/`.  
