---
layout: post
date: 2023/09/11 18:08 +0100
title: Opening files side-by-side in vim
excerpt: I had two text I wanted to view it's differences and I was already in vim. So, I decided to open both files side-by-side. This is what I did
---
I had two text I wanted to view it's differences and I was already in vim. So, I decided to open both files side-by-side. This is what I did:  

1. I created a new tab. In command mode, I typed `tabe` and hit enter.  
    *Tip:* To switch to command mode, from normal mode, type `:`.  
2. I opened the first file. `:e /tmp/1`.  
    *Note:* The `:` denotes command mode.  
3. I then opend the second file beside the first file: `:vsplit /tmp/2`.  

![A screenshot of vim displaying both open files](/images/2023-11-09-vim-screenshot.png)

## Further reading  

Check the help page for `split` (`:help split`). While you're there, type `gO` from normal mode to view the table of context. Perhaps something might catch your interest.  

Thank you for flying arfs6.me :)
