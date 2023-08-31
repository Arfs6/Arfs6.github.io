---
layout: post
title: "NvimPager"
category: neovim
excerpt: I have been using neovim as a pager for quite a while now. I use it for man pages, diffs and git logs. The only disadvantage of it so far is
date: 2023-08-05 21:44:00 +0100
---
I have been using neovim as a pager for quite a while now. I use it for man pages, diffs and git logs. The only disadvantage of it so far is that you can't open it unless standard input (stdin) reaches End-Of-File (EOF). This happens when you're reading from a program that might take a while before it finishes writing it's output. I hardly even encounter that. According to the project's README, "large files are slowing down neovim on startup". What about it's advantages? Well ... I get to use neovim as my pager. All the cool stuffs about neovim.  
## Installation  
You need `neovim` version 0.9 or later, `bash` (Most probably installed) and `scdoc` for man page.  

1. Neovim: The neovim wiki has a page on installing neovim for all platforms. I prefer the App Image one. Link: https://github.com/neovim/neovim/wiki/Installing-Neovim  
2. Bash: If you are using Linux, MacOS or WSL, you already have bash installed. I haven't tried installing nvim pager on windows.  
3. Scdoc: It is available on most package managers. Read [this](https://command-not-found.com/scdoc) for more info.  

Now, lets install nvimpager!  
```bash
# Create a directory to store the repo.
mkdir ~/repos
cd ~/repos # Switching to the created directory
# clone nvim pager's repo
git clone https://github.com/lucc/nvimpager
cd nvimpager # Go to nvim pager
make install
```  
This will install nvim pager to the default location on your system. To change the location, set the `PREFIX` variable to the  location. e.g. To install nvimpager to `~/.local`, run:  
```bash
make PREFIX=$HOME/.local
```  
## Usage  
`nvimpager file` to view a file in nvim pager or pipe a command to nvim pager: `command --help | nvimpager`. I have aliased nvimpager to np.  
Nvimpager has three mode:  
1. Pager mode: In this mode, the input is opened in neovim with read only mode. You can use all normal neovim commands that doesn't edit the buffer. To set pager mode, pass the `-p` option to nvim pager.  
2.  Cat mode: In this mode, all the input is written to your terminal's standard output (stdout). It will still have syntax highlighting To set cat mode, pass `-c` to nvim pager.  
3. Auto mode: This is the default. If the text can fit in your terminal, nvimpager uses cat mode. Otherwise, it uses pager mode.  
To pass neovim options to nvim pager, specify it after the `--` option. i.e. `nvimpager -- -u ~/nvim/init.lua`. On this note, nvimpager's configu files is different from that of neovim. That of nvimpager lives in `~/.config/nvimpager`. My nvimpager is focused on having very little startup time.  
Lastly, to use nvimpager as your default pager, you have to set the `MANPAGER` and `PAGER` environment variables to `"nvimpager"`. And `git config core.pager "nvimpager"` for git.  
## Note for Vim Users  
For vim users, you can checkout vimpager at https://github.com/rkitover/vimpager
