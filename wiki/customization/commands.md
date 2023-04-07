---
title: Commands
description: In-Game Commands of FancyMenu.
published: true
date: 2023-02-10T22:47:17.397Z
tags: 
editor: markdown
dateCreated: 2023-02-10T22:47:15.985Z
---

# 0. About

FancyMenu adds some commands to the game that can be very useful when combining them with other mods like quest mods.

# 1. Commands

All FancyMenu commands are normal slash (`/`) commands.

## openguiscreen

The `openguiscreen` command lets you open a GUI (vanilla/mod and custom GUIs).

**Usage:** `/openguiscreen <identifier>`

Replace `<identifier>` with the actual menu identifier of the GUI you want to open.
This can be the identifier of your custom GUI (made with FancyMenu) or the normal menu identifier of a vanilla/mod GUI.

> To get the **menu identifier of vanilla/mod GUIs**, open the menu and then click on **Tools -> Menu Info** of the FancyMenu customization bar at the top.<br>
This will show you the identifier in the **top-left corner**.
**Left-click the identifier to copy it to to the clipboard.**
{.is-info}

## closeguiscreen

The `closeguiscreen` command lets you close the current GUI.

Huh? This is totally useless you say?
Well yes, but actually no.

This command is useful for when using mods that trigger commands on specific actions.
So yes, this command is absolutely useless when using it without other mods, but can be really helpful if you have the right mods installed!

**Usage:** `/closeguiscreen`

## fmvariable

The `fmvariable` command allows you to set and get FancyMenu variables.

**Usage:** `/fmvariable <get_or_set> <variable_name> [<set_to_value>] [<send_chat_feedback>]`

### Get
To **get a variable value**, use the `get` sub-command like this:
`/fmvariable get some_variable`

Then the value of this variable will be printed to your chat.

### Set
To **set a varaible**, use the `set` sub-command like this:
`/fmvariable set some_variable new_value true`

The last argument here is to set if you want to receive chat feedback, which means if you want this command to print messages to your chat.
