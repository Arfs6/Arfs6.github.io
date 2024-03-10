---
layout: post
title: First Day On Linux Mint
date: 2024/03/09 08:58:00 +0100
category: linux accessibility
---
I spent the whole of yesterday playing around with [Linux Mint](https://linuxmint.com). With the help of a friend, I dual booted my laptop the day before yesterday (Friday). So far, everything works. I am trying to get used to using [orca](https://en.wikipedia.org/wiki/Orca_(assistive_technology)) (Linux's screen reader).

## The Installation Process

Installing Linux Mint was suprisingly easy. I thought I would need lots of sighted assistant, but I was wrong.

I installed Linux Mint by booting my laptop from a USB stick with linux mint on it and clicked the install icon on desktop. Since I was already running Linux Mint, I could turn on orca, although I didn't. The installation UI is a GUI, so orca would most probably work on it.

After the installation, my laptop now boots on Linux Mint directly. To run windows, I'd have to select it manually in the in-accessible bios interface. The process is relatively easy, although I don't like the fact that it's not accessible (or I don't know how to make it).

If you're wondering how I select windows in the menu, here is it:

- I start by holding escape key after turnning on my laptop and wait for a beeping sound.
- After which I will either press F9 or down arrow 4 times then enter.
- At this point, I will be presented with 3 options, the first one is ubuntu and the second one is windows. Since I want windows, I will press down arrow once and hit enter.

> The BIOS menu isn't the same for all computers.

It's the BIOS that I needed full sighted assistant with.

## Running Linux Mint

Tbh, it's not that different. The UI and screen reader were different, but I felt at home in the terminal and firefox. This is a very good thing.

There are lots of settings though. I am serious, there are lots of settings. It makes me think what a non-techy person will think about it.

Orca is different from [NVDA](https://nvaccess.org). I miss the helpful hot keys NVDA gives me, like `NVDA+Shift+b` to get my battery status. By the way, I use a cli (acpi) tool for checking my battery status :).

## Conclusion

So far, I haven't had any serious issue with Linux Mint. As a matter of fact, I am writing this blog post in [Neovim](https://neovim.io) on Linux Mint.

I think I'd have to read lots of docs to know where some stuffs are or how to do things like check battery status. With time, I'd get used to it.
