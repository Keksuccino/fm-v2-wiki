---
title: Custom Window Icon
description: Set a custom icon for the Minecraft window.
published: true
date: 2023-05-03T22:44:21.480Z
tags: customization
editor: markdown
dateCreated: 2023-04-07T04:31:28.064Z
---

# 0. About
As of v1.4, FancyMenu supports setting a custom Minecraft window icon.

# 1. Setting Up a Custom Icon
<br>

## 1.1. Creating the Icons
To set a custom icon, you first need to make two versions of your icon image.
The first one needs to be 16x16 pixels and the second one 32x32 pixels.

> **NOTE**: Only **PNG** images are supported.
{.is-info}

> **NOTE:** The icon has to be an **RGBA** image. The easiest way to do this is by adding some transparency to the icon (like transparent corners), but if you're familiar with image editing, export/save your image with an alpha channel (even if not needed). This will fix the issue. ([Here's how to force an alpha channel in GIMP](https://cdn.discordapp.com/attachments/795308330746511390/1091181963920023652/image.png))
{.is-warning}
 
## 1.2. Icon Names
In the next step, you need to rename your icon files.
The 16x16 icon needs to be named `icon16x16.png` and the 32x32 icon `icon32x32.png`.

## 1.3. Icon Directory
Now you have to navigate to FancyMenu's custom icon folder. This folder is located at `.minecraft/config/fancymenu/minecraftwindow/icons`.

Copy your icon files to this directory.

## 1.4. Enabling Custom Icons
The last step is to enable the **Custom Window Icon** option in the [FancyMenu settings](../mod-settings).

Now (re)start your game and stare at your success for a minimum of *5 minutes*!