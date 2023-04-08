---
title: Placeholders
description: Use placeholders to get things like the current time, screen width, the player name and much more.
published: true
date: 2023-02-11T01:00:06.302Z
tags: placeholder, text, replace, string
editor: markdown
dateCreated: 2023-02-11T01:00:03.750Z
---

# 0. About

This page focuses on placeholders, which can be used in most places where the user can input a value (like text or numbers).

Placeholders get replaced with their actual value and get updated every game tick.

# 1. Using Placeholders

To use placeholders, click on the little "Plus" button (+) at the right side of text input fields.

![Screenshot_1](https://user-images.githubusercontent.com/35544624/218228337-f60af4fa-3aac-41d2-bdbc-14ee1bd17a39.png)

> If there is no "Plus" button at the right side of the text input field, placeholders aren't supported for that value.
{.is-warning}

Clicking on the button will open a context menu where you can see all placeholders.
You can **left-click on placeholders** to **paste** them to the text input field.

![Screenshot_3](https://user-images.githubusercontent.com/35544624/218228360-41511037-f453-4c11-a2d1-9cefa9649583.png)

# 2. Nested Placeholders

Some placeholders need you to specify variable values to work properly. It is possible to use placeholders **in** these values.

So for example, it is possible to use placeholders as part of the expression value of **Calculator** placeholders:

`{"placeholder":"calc","values":{"expression":"{"placeholder":"guiwidth"} / 2","decimal":"false"}}`

This **Calculator** placeholder uses the **Screen Width** placeholder in its expression value.



