---
layout: post
title: My math workstation
categories: latex vim nvda
tags: latex, nvda, mathml, mathjax, neovim, vim
excerpt: My LaTeX setup
date: 2023-11-05 13:27 +0100
---
As a computer science student, I take courses with calculations in it. I am in the process of building my "workstation" or "schoolstation" for learning and writing such courses. This post is for me to share how my work station is, It might be useful for other people who are also trying to figure out what tools to use.  

I'll be dividing this post into three:  

1. [Writing](#writing)  
2. [Transpiling](#transpiling)  
3. [Reading](#reading)  

## Writing {#writing}  

This step involves writing the LaTeX document. I started using [access8math](https://github.com/tsengwoody/Access8Math) for writing the TeX document. With time, I gradually moved to [neovim](https://neovim.io) for the writing part, and I am now fully using it to write my LaTeX "code".  Neovim had a lot more to offer.  

I use neovim in [wsl](https://learn.microsoft.com/en-us/windows/wsl/about), but it works in windows as well. I just tend to spend more time in wsl. If you're interested in neovim and want to try it out, here is it's installation guide: <https://github.com/neovim/neovim/wiki/Installing-Neovim>. I don't know which tutorial to suggest, I used the builtin vim tutor.  

Here are the plugins and features of neovim I use:  

- **[Marks](https://vim.fandom.com/wiki/Using_marks)**: This lets me to mark a section in the file I am editing. It allows me to jump from one part of the document to another. E.g. From the question to the solution.  
- Jump to next or previous method. This is a command in vim that jumps to next or previous methods. In LaTeX document, it will jump to next or previous environment. E.g. `\begin{equation}` environment. This is very useful when navigating the file. `[m` jumps to previous environment and `]m` jumps to next environment.
- **[vimtex](https://github.com/lervag/vimtex)**: This is a plugin that adds better support for LaTeX in vim. It has a lot of features. E.g. You can use `%` to jump between the start and end of an environment.  
- A custom script that transpiles (compiles) my LaTeX document to HTML when I save the file. The script is very simple, it just calls `pandoc` and passes the appropriate arguments for the conversion. I would write a different blog post on how to do that.  

This aren't all the features I use, I'll add more with time.

## Transpiling {#transpiling}  

The two formats I usually transpile LaTeX to are pdf and HTML. As for the pdf, I use pdflatex, which comes with most LaTeX distributions.You can get a LaTeX distribution here: <https://www.latex-project.org/get/>. As for the HTML conversion, I use pandoc. Pandoc is a document converter. You can install one by visiting this page and following the instruction as per your operating system: <https://pandoc.org/installing.html>  

Both pandoc and pdflatex are command line tools. Here are the commands I use to transpile to HTML:  

```bash
pandoc -f latex -t html --mathml -o file.html file.tex
```

Where `file.tex` is the LaTeX file and `file.html` is the file to store the HTML output in. The `--mathml` tells pandoc to convert it to mathml, you can use `--mathjax` to convert it to mathjax.  

Here is the command I use to convert to pdf:  

```bash
pdflatex file.tex
```

Where `file.tex` is the LaTeX file. On successful compilation, `pdflatex` stores the pdf output in `file.pdf`. It changes the extension of the input file from `.tex` to `.pdf`. I haven't figured out what to do when there is an error in my LaTeX, I just abort the process by pressing ctrl+d and going back to neovim to figure it out.  

## Reading {#reading}  

This section might not be useful to sighted people. As a blind person, I have to figure out how to read the math I wrote. While writing, I read the LaTeX text directly. After I am done writing, I usually want to cross check what I wrote. For this step, I convert the LaTeX document to HTML, then open it in my browser (Microsoft edge for now).  

I am an [NVDA](https://www.nvaccess.org/) user. For me to be able to read math in my browser, I need a math player. I have both [access8math](https://github.com/tsengwoody/Access8Math) and [mathcat](https://addons.nvda-project.org/addons/MathCAT.en.html). I have been using mathcat lately though.  

## Conclusion  

This is my workstation for LaTeX. I will try to update this post as it evolves. If you have any suggestion or comment, don't hesitate to contact me using any of the options at the bottom of this page.  
