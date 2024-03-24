---
layout: post
title: A Tip To Make Your Website More Accessible
date: 2024/03/24 22:21:00 +0100
category: accessibility
---
Unless you're doing some crazy stuffs with javascript and html div tags, your website should be accessible. But, there are some stuffs we do in css or js that never reaches a screen reader user. Here is a rule of thumb you can use to take care of that:

> Whatever you do visually in css or js, make sure you're using the right html tags.

Here are some examples to illustrate what I mean:

1. If you have added a border to some elements, consider using a container html. There are tags for headers, footers, sections and navigations.
2. If you show an element on hover with mouse, consider using a [summary tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/summary).
3. Consider using a proper [dialog element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dialog) instead of manually creating one with js and css.

These are common accessibility problems I have seen with websites that could be fixed by just using proper html.
