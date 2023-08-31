---
layout: post
title: Commands, Motions and Text Objects in vim
date: 2023/08/14 17:32:00 +0100
categories: vim
tags: neovim vim
excerpt: I made an awesome discovery recently on vim. It was by accident. So, here is the jist
---
I made an awesome discovery [recently](https://twitter.com/arf_s6/status/1690108353614131200?s=20) on vim. It was by accident. So, here is the jist:  
## TL;DR  

| before         | insert | after |
|:---------------|:-------|:------|
| `"hello |world"` | `ci"`    | `"|"`  |
| `| "hello world"` | `ci"`   | `"|"`  |

The `|` character represents your cursor position. Notice how it is placed between the `quotes` after the command.  

## Full Jist  
If you don't know what `w`, `y` or `/` does in vim, I'll suggest trying out [vimtutor](https://linux.how2shout.com/how-to-open-vimtutor-in-neovim-and-vim-commands/). Very hepful!  
Now, let's break down the above commad (`ci"`).  

### Synopsys  

__Normal mode__: `\<operator-pending-command\>[<inner/A\>]<motion|text-object\>`  
Breakdown:  

- `c`: operator-pending-command - These are commands that requires a motion or text object to operate on. They include `y`, `d` and `c`.  
- `i`: [optional] inner. You can use either `i` for inner or `a` to include delimiteres if any. For text objects, I think it is compulsory. It has a specific effect with motions (explained later).  
- `"`: text-object - This is a text object. i.e. The quotes and everything within it. Other text objects include `(`, `{` and `'.  
- `w`: motion - Any motion. e.g. `w`, `j` or `s`.  

### Explanation  

These are normal mode commands. Just type `<ESC>` from which ever mode you are to go back to normal mode and execute the commands.  
`Operator-pending` commands are commands that needs more information before it can execute it's action. e.g. When you want to delete a text in vim, the command is `d`. But how will vim know what you want to delete? Tell it! You have a lot of options. You can use `motions` to delete "motionwise". i.e. `dw` to delete word, or `d$` to delete to the end of the line. Another option is to specify a text-object.  
Now, `text-objects` is a fancy word for group of text . It could be a sentence (`s`), a paragraph (`p`),  or method (`]m`). The `"` in the above example represents text withing quotes.  
What about the `inner (i)|A (a)` part? Normally, when you specify a motion, it starts from the position of your cursor. But with `i (inner)` and `a (A)`, you can perform the action on the whole ... motion / text-object. i.e. `iw` means inner word, excluding spaces around. It works for both text-objects and motions. Let me show you the difference.  

| before          | insert     | after   |  
| :--------------- | :---------- | :------- |  
| `"hello |world`" | `ds` | `hello |` |  
| `hello | world` | `dis` | `|` |  

Without `i` or `a`, the action is executed starting from your cursor position. With `i` or `a`, context is included.  

### Step by step guide  

- Open vim: `vim file.txt`.  
- Go to insert mode: `i`.  
- Type some text: `"Hello Vim World!"`.  
- Go back to normal mode: `\<ESC\>`.  
- Execute command: `ci"`.  

### Examples  

I like examples. So, let me give you some:  
- `ci"`: Change text `in`side quotes.  
- `yis`: Yank / copy whole sentence.  
- `di(`: Delete everything inside the parentheses.  
- `diw`: delete the entire word.  
- `=i}`: Format everything between braces (`{}`).  
- `saa"(` Using sandwich plugin, wrap the things inside the quotes with parentheses.  i.e. "hello world" => `saa")` => ("hello world").  

#### Over Here 
You can use `/` also. e.g. `d/`. When you timepress `/`, it will open the search area for you to type something to search. When you click enter, it will perform the action  from your current cursor position to the first result of your search. This one was unexpected for me. I knew about using `n` but not `/`. Wonders of vim 😀  

## Conclusion  

At the end of the day, if you don't practice / try these commands, you will forget it all. But if you keep practising, it will become second nature!  
If you found the post informative, please tell me on mastodon or twitter. Links below. Also, feedback and suggestions are welcomed.  
