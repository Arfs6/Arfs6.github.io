---
layout: post
title: WSL Not Responding
date: 2023/12/22 08:26:00 +0100
category: wsl
excerpt: After turning on my laptop (desktop 😀), wsl will not respond to any command
---
This is the second time I am having this problem. After turning on my laptop (desktop 😀), WSL will not respond to any command. It will hang indefinitely. This time, I am going to share how I "solved" it.

There is an [issue](https://github.com/microsoft/WSL/issues/8529) on the WSL github repo on this problem, but it seems there is a difficulty reproducing the bug. A temporary solution [suggested](https://github.com/microsoft/WSL/issues/8529#issuecomment-1166352159) by[mmichal3](https://github.com/mmichal3) is to kill the WSL process from task manager.

## Solution: Kill WSL Process

You can kill the WSL process the task manager way, but I prefer using CLI for this, as it's more precise. The command for killing a process on windows is `taskkill` and `tasklist` is for listing all running processes.

If you run `tasklist` in powershell, you'll see 3 different processes that are related to WSL:

1. `wsl.exe`
2. `wslhost.exe` and
3. `wslservice.exe`

> Side note: I was shocked at the amount of processes running when I executed `tasklist`.

The process you want to kill is `wslservice.exe`. You need an elevated powershell to be able to kill it and you have to forcefully kill it.

To get an elevated powershell, press windows button and search for `powershell`. Then right click and click on run as administrator.

Here is the command to forcefully kill `wslservice.exe`:

```bash
taskkill -F -IM wslservice.exe
```

With this, you can open your WSL the way you are used to, and it will hopefully work.
