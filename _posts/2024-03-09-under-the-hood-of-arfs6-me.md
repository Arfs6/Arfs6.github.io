---
layout: post
title: Under The Hood Of arfs6.me
category: programming
date: 2024/03/09 13:24:00 +0100
---
The two main things under arfs6.me are [github pages](https://pages.github.com/) and [jekyll](https://jekyllrb.com/).

## [Github pages](https://pages.github.com/)

Github pages is a feature of github that makes a repo a website. Just `git add`, `git commit` and `git push` and your website is live! You can enable it for a repo in it's settings page, mine is at [arfs6/afs6.github.io](https://github.com/arfs6/arfs6.github.io).

[More info](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages)

> An alternative is [netlify](https://www.netlify.com/), they have a free plan.

## [Jekyll](https://jekyllrb.com/)

Jekyll is a static site generator, you give it bits of pages and it generates the static file for the website. This blog post is a [markdown document](https://github.com/Arfs6/Arfs6.github.io/blob/raw/_posts/2024-03-09-under-the-hood-of-arfs6-me.md) that jekyll will convert to html and insert it into the post template. I use [github actions](https://github.com/features/actions) to build the website.

[More info](https://jekyllrb.com/docs/)

> An alternative is [hugo](https://gohugo.io/), I think it's main selling point is speed.

## Putting it all together:

Here is an [article](https://chrisjhart.com/Creating-a-Simple-Free-Blog/) that will help you setup github pages + jekyll in just a few minutes. Both jekyll and github pages have been around for years, so there are lots of info about them online.
