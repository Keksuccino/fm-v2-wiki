---
title: Button Scripts
description: Run button scripts by pressing a custom button.
published: true
date: 2023-02-10T22:47:01.711Z
tags: advanced
editor: markdown
dateCreated: 2023-02-10T22:46:59.729Z
---

# 0. About

As of version 1.5, FancyMenu supports executing multiple [button actions](../customization/custom-buttons#h-2-button-actions) per button click.
This is possible by creating a button script containing all button actions you want to run by clicking the custom button.

# 1. Creating a Script

Buttons scripts are located in `.minecraft/config/fancymenu/buttonscripts`.
To keep it as simple as possible, button scripts are simple text files (.TXT files), allowing you to edit them with every text editor.

Creating a button script is very easy. It's basically just writing multiple [button actions](../customization/custom-buttons#h-2-button-actions) as list (one action per line).

The [button action](../customization/custom-buttons#h-2-button-actions) and its value (if there is one for the specific button action) are going to the same line, separated by colon (`:`).

A working button script to rename customization files and reload the menu (to switch between layouts by button click) can look like this:

```
renamefile:config/fancymenu/customization/layout.txt;layout.temp
renamefile:config/fancymenu/customization/layout.disabled;layout.txt
renamefile:config/fancymenu/customization/layout.temp;layout.disabled
reloadmenu
```

The code above is all the script needs to work, nothing special. The part before the colon is the [button action](../customization/custom-buttons#h-2-button-actions), everything after the colon is its value.
The `reloadmenu` [button action](../customization/custom-buttons#h-2-button-actions) has no value, that's why there's no colon on this line.

When you're done writing your script, just save it to the `buttonscripts` directory (mentioned above), with whatever name you like. Just be sure that it has the **TXT** file type.

After you've saved your button script, simply press the [Reload button](../customization/customization-helper#h-1-the-reload-button) to load the new button script into FancyMenu and you're done.

# 2. Using Button Scripts

Button scripts can be executed by using the [`runscript`](../customization/custom-buttons#runscript) button action.
The value for this [button action](../customization/custom-buttons#h-2-button-actions) is the script file name **without the file extension**. So if you've named your button script `myscript.txt`, the button action value would be `myscript`.