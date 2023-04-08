---
title: Custom Buttons
description: Create custom buttons and use them to open menus, links and more.
published: true
date: 2023-02-10T22:47:21.294Z
tags: customization
editor: markdown
dateCreated: 2023-02-10T22:47:20.001Z
---

# 0. About

You can create custom buttons for menus and specify what they do.
There are some very useful button actions you can attach to them to let them open links, join servers, sending commands and much more!

# 1. Creating Custom Buttons

To add a custom button to a menu, you need to [create a new layout for it](./customization-helper#h-22-layouts).

When you're in the [Layout Editor](./layout-editor), just [add a new button element](./layout-editor#h-213-element) to the layout.

Now you can **right-click** the new button to set what it should do when clicking on it, by using the **Button Action** option.

# 2. Button Actions
<br>

## openlink
Open a link in your default browser.

| Value needed? | Value content | Value Examples                  |
|---------------|---------------|---------------------------|
| Yes           | The link      | `https://google.de` |

## sendmessage
Send a message or a command to the chat.

| Value needed? | Value content       | Value Examples                                               |
|---------------|---------------------|--------------------------------------------------------|
| Yes           | The message/command | `Hi everyone!`<br>----<br>`/time set 0` |

## quitgame
Quit minecraft.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| No            | /             | /        |

## joinserver
Join a minecraft server.

| Value needed? | Value content | Value Examples                                                   |
|---------------|---------------|------------------------------------------------------------|
| Yes           | The server IP | `127.0.0.1:25565`<br>----<br>`play.hivemc.com` |

## loadworld
Load a minecraft world (from the client's playable minecraft worlds).

| Value needed? | Value content         | Value Examples                                       |
|---------------|-----------------------|------------------------------------------------|
| Yes           | The world **folder** name | `My World`<br>----<br>`cool_world` |

## openfile
Open a file or folder.

| Value needed? | Value content               | Value Examples                                                    |
|---------------|-----------------------------|-------------------------------------------------------------|
| Yes           | The path to the file/folder | `mydata/info.txt`<br>----<br>`images/minecraft` |

## movefile
Move a file to a new path.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| Yes           | The old file path and the new file path, separated by semicolon (`;`). | `path/to/file.txt;new/path/of/file.txt` |

## copyfile
Copy a file.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| Yes           | The path to the file and the path to copy it to, separated by semicolon (`;`). | `path/to/file.txt;copy/to/path/filecopy.txt` |

## deletefile
**Completely** delete a file.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| Yes           | The path to the file. | `path/to/file.txt` |

## renamefile
Rename a file.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| Yes           | The path to the file and its new name, separated by semicolon (`;`). | `path/to/file.txt;newfilename.txt` |

## downloadfile
Download a file from the web.
This action runs in the main thread, which means it will cause the game to freeze until it is done.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| Yes           | The URL to the file and the path to save it to, separated by semicolon (`;`). | `https://myhoster.com/archive.zip;path/to/save/archive.zip` |

## unpackzip
Unpack a ZIP file.
This action runs in the main thread, which means it will cause the game to freeze until it is done.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| Yes           | The path to the ZIP file and the directory to unpack it to, separated by semicolon (`;`). | `path/to/archive.zip;unpack/to/path/` |

## prevbackground
Switch to the previous menu background animation.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| No            | /             | /        |

## nextbackground
Switch to the next menu background animation.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| No            | /             | /        |

## opencustomgui
Open one of your [custom GUIs](../advanced/custom-guis).

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| Yes           | The custom GUI identifier | `mycoolmenu` |

## opengui
Open an existing GUI by its menu identifier.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| Yes           | The menu identifier (Get it by clicking on the "Menu Info" button in menus) | `the.menu.identifier` |

## reloadmenu
Reload the current menu along with reloading customization files, the mod config, button scripts and more.
This action is similar to clicking the "Reload" button in the top-right corner of supported menus.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| No            | /             | /        |

## runscript
Run a [button script](../advanced/button-scripts).

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| Yes           | The file name of your script, without the file extension. | `myscript` |

## mutebackgroundsounds
Mute or unmute background audio added by FancyMenu.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| Yes           | true/false (to mute or unmute the audio) | `true` |

## runcmd
Run a CMD/Terminal command.
Supports per-OS commands to set different commands for different operating systems.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| Yes           | The command. | `start_server.bat`<br>-----<br>`[linux:./start_server.sh];[windows:start_server.bat];` |

To set separated commands for different operating systems, just format your value like this:
`[windows:start.bat];[macos:./start];[linux:./start.sh];`

This will run the command `start.bat` on Windows, the `./start` command on macOS and the `./start.sh` command on Linux.

It's important to put every command section in brackets (`[ ]`) and to separate every section with a semicolon (`;`).

## closegui
Close the current menu/GUI.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| No           | / | / |

## mimicbutton
Mimic the button action of an vanilla button.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| Yes           | Button Locator of target button | `some.menu.identifier:23938` |

To use this action, you need to get the **button locator** of the target vanilla button you want to mimic.

The **button locator** is basically just a combination of the identifier of the menu the button is part of, and the ID of the button, separated by colon (`:`).

To get the menu identifier of the menu of the button, just use the [Menu Info](./customization-helper#h-41-menu-info) tool.
Then use the [Button Info](./customization-helper#h-42-button-info) tool and hover over the target button, to see its button ID.

> If you've used the layout editor to copy the button ID, don't forget to remove its `vanillabtn:` prefix.
You only need the number part in this case.
{.is-warning}

Now combine the menu identifier and button ID like this:
`menu_identifier:button_id`

This is your button locator. Use this locator as value for the `mimicbutton` action and you're done!

## join_last_world
Join the last active world/server.

> Only available in FancyMenu v2.6.6+!
{.is-warning}

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| No           | / | / |

## set_variable
Store/set a variable and use it in placeholders and visibility requirements.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| Yes           | Variable name and value | `some_variable:3` |

## clear_variables
Delete/clear ALL stored variables.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| No          | / | / |

## paste_to_chat
Paste something to the chat text field.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| Yes          | Append True/False and text to paste | `true:How are you?` |

If **append** is `true`, it will add the text to the existing content of the chat text field. If it's `false`, it will replace the old content with the new one.

## toggle_layout
Toggle (enable/disable) a menu layout.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| Yes          | Layout Name | `some_cool_layout` |

## enable_layout
Enable a menu layout.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| Yes          | Layout Name | `some_cool_layout` |

## disable_layout
Disable a menu layout.

| Value needed? | Value content | Value Examples |
|---------------|---------------|----------|
| Yes          | Layout Name | `some_cool_layout` |





