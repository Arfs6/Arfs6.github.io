---
layout: post
title: A To Z In Vim
date: 2023/11/17 18:52:00 +0100
category: vim
excerpt: I'll be writing this from memory, no help pages, no googling!
---
In this post, I'll be writing what each alphabet on my keyboard means in normal mode of vim. Instead of going from **a** to **z**, I'll follow the layout of my keyboard (quarti).

I'll be writing this from memory, no help pages, no googling! I don't know all the upper case commands, so this list will contain only lower case characters.

1. **q**: Records a macro. You must give it a register (character) to store the macro in it.
2. **w**: Go to the next `word`.
3. **e**: Go to the end of the current word.
4. **r**: Replace the character under your cursor with another one. Type the replacement after typing the command.
5. **t**: Till next occurrence of a character. Must type character after command.
6. **y**: Copy / Yank. Must give text object or motion to copy.
7. **u**: Undo.
8. **i**: Switch to insert mode.
9. **o**: Create a new line below the focused line and switch to insert mode.
10. **p**: Paste.
11. **a**: Switch to insert mode with cursor after the currently focused character.
12. **s**: Delete the current character and switch to insert mode.
13. **d**: Delete. Must pass text object or motion to delete.
14. **f**: Go to the previous occurrence of a character. Must type character after command.
    > I got this wrong. It's `F` that goes to previous, `f` goes to next occurance with the cursor on the character. E.G. `fa` will go to the next occurance of `a` and place your cursor on `a`.
15. **g**: Like a modifier. Characters typed after it has meaning. E.G. `gg` move to top. Mostly motion related commands.
16. **h**: Previous character.
17. **j**: Next line.
18. **k**: previous line.
19. **l**: Next character.
20. **z**: Like **g**.
21. **x**: Delete the character under the cursor.
22. **c**: Deletes a text a switch to insert mode. Must pass text object or motion to delete.
23. **v**: Switch to visual mode.
24. **b**: Go to the start of the currently focused word. If already at start, go to the start of the previous word.
25. **n**: Go to the next search result.
26. **m**: Mark cursor position. Must specify register (character) to store mark in. Upper case registers are global and numeric registers are overriding at vim startup.

## Impressive?

It took me months to reach this point. This twitter [tweet](https://twitter.com/arf_s6/status/1632059902033051650?t=m_jcyAFRlWkS06MfzOGU9Q&s=19) was like weeks after I started.

I found new commands by mistake, I found other commands by reading. It just compiled over time and now, it is a muscle memory.
