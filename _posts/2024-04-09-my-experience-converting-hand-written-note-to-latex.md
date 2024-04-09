---
layout: post
title: My Experience Converting Hand Written Notes To LaTeX
date: 2024/04/09 21:42:00 +0100
category: latex
---
Recently, I had to convert 60 pages of hand-written note to LaTeX. The notes has math in it, it was a physics note. I didn't want to write everything from scratch, plus getting someone to read everything won't be easy. So, I tried gemini, llava, mathpix and mathkicker. All these are so-called AIs.

I started by asking a friend to take a picture of all the pages of the notes, then I renamed the files with my brothers help. This allowed me to independently try multiple options.

## [Gemini](https://gemini.google.com)

The first AI I tried was gemini. I have grown used to it for certain tasks, because it's better than chat GPT in some tasks.

It refused to convert it at my first request, saying something within the lines of; _"I can't do this for you because you're blind"_. Yeah, I told it I am blind, hoping it won't hallucinate.

I then stripped out the _"I am blind"_ part in the prompt and tried again. It gave me a LaTeX output which I showed to a sighted person. The person confirmed it was correct, so I proceeded to convert all the other pages with the same prompt.

After converting about 2 dozens, I had a suspicion it was hallucinating. I opened it in a new tab, asked it to convert it again and I got a different output from the one I had. It turns out, I had been saving hallucination all along.

> I have a feeling chat gpt will perform better than gemini, but I couldn't try chat gpt because I don't have access to the model that can understand image.

## Llava

Llava is an open source model that can understand pictures. I tried working with it on hugging face but it generated partial output. I spent hours, like hours, I mean hours, trying to make it work but I couldn't. I have learnt a couple of things though. Stuffs like gradio and ollama.

## [Mathpix](https://mathpix.com)

I learnt about mathpix and mathkicker from my online friends. I have played with both, but I have never done anything useful with it before now.

Mathpix is payed. It has a restriction of 10 pages per pdf, and I think that is all you can get for free.

The 10 pages I converted was from a different pdf, it is a statistics hand written note. I liked the how it gave me multiple options for the output, and it's output was nice.

Unfortunately, it couldn't help me with this notes, so I proceeded to

## [Mathkicker.ai](https://mathkicker.ai)

Mathkicker.ai was built specifically to help blind student convert pictures and PDFs to Microsoft docx or html, and it's free.

The first output format I tried was html because I was more familiar with it. Fortunately, it worked without hallucination. Unfortunately it was rendering the math as pictures, svg to be specific. I was running from pictures just to end up on a different format of pictures 😂. I tried converting the html file to LaTeX, and without any surprises, it didn't work. So I settled for it and converted all the notes to html. I was thinking of re-writing the math part myself.

Out of curiosity, I tried the Microsoft docx output. The math sounded horrible with NVDA, it was reading each math character as numbers, something like _"1, 2, 4, 6"_. Docx is an unknown territory for me, so I switched to html. The MathML version of the docx file sounded the same, with the same strange reading of the math. Fortunately, the mathjax version worked, and the math was readable at last. There were typos and errors, but I had already anticipated that. I haven't finished fixing it yet.

> Pandoc has been a saviour a lot since I started learning LaTeX.

## Conclusion

From picture to mathkicker.ai to docx to html / mathjax via pandoc and to latex via pandoc too. This is the way I'll be converting hand written notes to LaTeX from now on.

It took me days to reach this conclusion. I learnt a lot, and I hope you have also learnt something.

As always, you can always shoot me an [email](mailto:arfs6.mail@gmail.com) if you want to tell me anything.

Peace ✌
