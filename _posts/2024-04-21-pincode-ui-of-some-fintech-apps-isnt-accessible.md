---
layout: post
title: Pincode UI Of Some Fintech Apps Isn't Accessible
date: 2024/04/21 17:19:00 +0100
category: accessibility
---
A wise man once said: _"The only truly secure system is one that is powered off, cast in a block of concrete and sealed in a lead-lined room with armed guards."_ - **Gene Spafford**. What is the point of a highly secured pin code UI (User Interface) if it's not useable?

I am talking about the UI that seems to use a frame with a background picture that looks like buttons. Input is gotten from users by listening for touch events at specific coordinates. This is what I'll do if you ask me to re-create a similar UI. I might be wrong about the implementation, but this is how it feels to me as a screen reader user. The UI is going to be absolutely in-accessible to screen readers and voice control.

> **FYI**: Screen readers read what is on the screen for blind people while voice control let you use your voice to control your phone.

The reason why developers don't use the default keyboard by mobile phones seems to be because of trust, they can't trust the developers of the keyboard not to snoop the password. So, fintech apps create custom UI to handle input from users. The problem lies in the solution some devs choose.

In pursuit of security, they make a UI that isn't accessible to screen readers and voice controls. It's mostly out of ignorance. The most accessible solution is to create a **4X3** grid of buttons with labels.

I can't understand why someone will develop a UI with frame + picture + touch event, instead of using buttons????? From my point of view, it's easier to make a **4X3** grid of buttons, instead of listening for touch events at specific coordinates. Using buttons is more accessible, as long as the buttons have labels. This is what a lot of bank apps use, this is what android does in there lock screen. The frame + background picture + touch event will be more difficult to maintain.

I am not a security person, but I see no difference in the security of the UI with frame + background picture + touch events vs a grid of buttons. Both are vulnerable to [keyloggers](https://en.wikipedia.org/wiki/Keystroke_logging).

You don't want to know the number of fintech apps I have ditched because there pincode area isn't accessible. Most times, it's only the pincode area that isn't accessible, everything else is accessible. If the pincode area isn't accessible, it's like the whole app isn't accessible to me.
