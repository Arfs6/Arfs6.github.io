---
layout: post
title: A Tip For Making Your website More Accessible
date: 2024/03/24 22:21:00 +0100
category: accessibility
---
Unless you're doing some crazy stuffs with javascript and html div tags, your website should be accessible. But, there are some stuffs we do in css or js that never reaches a screen reader user. Here is a rule of thumb you can use to take care of that:

> Whatever you do in css or js, make sure you're using the right [html elements](https://dev.to/polgarj/a-short-guide-to-help-you-pick-the-correct-html-tag-56l9).

Here are some examples to illustrate what I mean:

1. If you have added a border or shadow to a group of text, consider using a container html. There are tags for headers, footers, sections and navigations.
2. If you show an element on hover with mouse, consider using a [summary tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/summary).
3. Consider using a proper [dialog element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dialog) instead of manually creating one with js and css z-index.
4. If you want to accept input by clicking, make sure you're using the right html element (input, button, ...) or you're adding proper [aria attributes](https://stackoverflow.com/questions/32659099/making-a-clickable-div-accessible-through-tab-structure).

These are common accessibility problems I have seen with websites that could be fixed by just using proper html. Screen readers rely on proper html elements or aria attributes to get info about a html element. If you style a div like a dialog but you don't use the right html tags and attributes, it will appear like any other text in the page to a screen reader user.

Here is a nice article that will help you pick the right html element: [A short guide to help you pick the correct HTML tag - DEV Community](https://dev.to/polgarj/a-short-guide-to-help-you-pick-the-correct-html-tag-56l9).
