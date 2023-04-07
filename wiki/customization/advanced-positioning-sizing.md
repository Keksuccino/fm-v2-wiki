---
title: Advanced Positioning & Sizing
description: Have full controls over size and position of your elements by using advanced positioning/sizing.
published: true
date: 2023-02-11T01:00:24.662Z
tags: advanced, button, element, position, size, manual, manually
editor: markdown
dateCreated: 2023-02-11T00:41:24.878Z
---

# 0. About

This page focuses on the advanced positioning/sizing of elements, added in FancyMenu v2.13.0.

Advanced positoning/sizing allows you to have **full control over the position and size of your elements**. This is very powerful but also **a lot more time-consuming** than using FancyMenu's automated sizing and positioning.

# 1. Toggling Advanced Positioning/Sizing Mode

<br>

## 1.1. Enabling Advanced Positioning/Sizing

To enable andvanced positioning/sizing for an element, **right-click** it and click on **Advanced Positioning** or **Advanced Sizing**.

The element will automatically switch to the advanced mode when you set an advanced position or size value.

> While an element is in this mode, you will **not be able** to **resize** it by using the grabbers at the element edges or **moving** it by grabbing it.
{.is-warning}

## 1.2. Disabling Advanced Positioning/Sizing

To disable it and switch back to normal positioning/sizing, **clear all positioning/sizing values**.

# 2. Calculating Positions/Sizes

The reason why advanced positioning/sizing is so powerful is that you can use **placeholders** in the position/size values.

> You can see all placeholders by clicking on the little "Plus" button (+) at the right side of text input fields. Click on a placeholder in the placeholder menu to paste it to your text input field.
{.is-info}

This allows you to use the **Calculator** placeholder (located in the **Advanced** category) in combination with placeholders of the **GUI** category, like **Screen Width**, **GUI Scale**, **Element Width** and much more.

![Screenshot_9](https://user-images.githubusercontent.com/35544624/218225109-dcf8d16c-9c79-4264-97f7-d30b903063ed.png)

To calculate something with the **Calculator** placeholder, replace the example expression with your own. You can use **placeholders in the expression**, which makes it possible to get, for example, the screen size or position and size of elements.

For example, this placeholder will simply solve `1 + 1` and will show as `2` later:

`{"placeholder":"calc","values":{"expression":"1 + 1","decimal":"false"}}`

The `decimal` variable is set to `false`, which is important for most sizing/positioning calculations, so just set this always to `false` when working with advanced positioning/sizing.

The following calculator uses the **Screen Width** placeholder and divides it by `2`:

`{"placeholder":"calc","values":{"expression":"{"placeholder":"guiwidth"} / 2","decimal":"false"}}`
