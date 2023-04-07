---
title: Text Formatting
description: Change the color and size of text.
published: true
date: 2023-02-10T23:14:44.335Z
tags: customization
editor: markdown
dateCreated: 2023-02-10T22:47:41.444Z
---

# 0. About
FancyMenu allows you to change the text formatting of all elements allowing for text input (like normal texts, web texts and button labels).
You can change the text color, make it bold, underlined and more.

It also allows you to change the text scale (size) of most of the text-based elements.

# 1. How to Format a Text
FancyMenu uses Minecraft's built-in text formatting system.
This system works with simple formatting codes like `&6` or `&l`.

These formatting codes can be inserted in texts to change everything **after** the formatting code to the specific formatting.

A list of all formatting codes along with a detailed description of how to use these codes can be found in the [official Minecraft wiki](https://minecraft.fandom.com/wiki/Formatting_codes).

> **IMPORTANT**: The Minecraft wiki will use `§` as formatting code prefix, but FancyMenu needs the alternative code format, so please use `&` instead of `§` in FancyMenu!
{.is-warning}

For example, `&cThis is a &ecolored text.` will show `This is a` as red text and `colored text.` as yellow text, because `&c`, the formatting code for red, is written before `This is a`, so everything after this formatting code will be red, until another formatting code is used. In this case, red is replaced with yellow after using `&e`, the formatting code for yellow.

# 2. How to Change the Text Scale

Not all, but most of the text-based elements allow you to set its **text scale**.

If the element has this setting, you can find it by rightclicking the element and searching for something like a **Scale** or **Text Scale** option in the context menu.

The default Minecraft text scale is `1.0`, that's the scale of nearly all default texts in Minecraft.
A scale of `2.0` will double the text size and a scale of `0.5` will half it.

# 3. Line Break / Multi-Line Text

Text elements (not all text-based elements, just actual text elements) support line breaks, which means you can make elements with more than one line.

To render text on a new line, type `\n` in the content text field.
Everything after this code is rendered on the next line.

Keep in mind that the line break is only visible in the actual element, not while editing the content of the element.