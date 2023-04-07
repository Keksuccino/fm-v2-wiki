---
title: Custom GUIs
description: Create completely new GUIs and fill them with content.
published: true
date: 2023-02-10T22:47:03.672Z
tags: advanced
editor: markdown
dateCreated: 2023-02-10T22:47:02.358Z
---

# 0. About
As of version 1.4, FancyMenu supports creating custom GUIs.
You can open them by clicking a button or override existing menus with them.

> **NOTE:** The controls to create custom GUIs are **disabled** by default.
You will need to enable the **Advanced Mode** in the [FancyMenu Settings](../Mod-Settings) first.
{.is-info}

> **IMPORTANT:** Please note that it is **not recommended** to override existing GUIs with custom ones!
If you want to customize an existing menu, [use a layout](../customization/customization-helper#h-22-layouts) instead!
{.is-warning}

# 1. Creating a Custom GUI
To create a new GUI, navigate to the [Custom GUIs](../customization/customization-helper#h-3-managing-custom-guis) tab in the [Customization Helper](../customization/customization-helper) and click on **New**.

![new-custom-gui](https://user-images.githubusercontent.com/35544624/111208704-638d6c00-85cb-11eb-81c7-047dbbf95916.png)

This will open a popup where you can set all important stuff for your new GUI.

## Menu Identifier
This is the **unique** identifier for your menu.
It is needed when you want to open your GUI with a [custom button](../customization/custom-buttons) later or when you want to override a menu with it.

## Menu Title
The menu title is optional and will be shown at the top of your menu, just like in many vanilla menus.

## Allow ESC
Enabling this will allow users to close your menu by pressing the **ESC** key.

# 2. Adding Content to Custom GUIs
Custom GUIs can be filled with content just like you customize normal Minecraft menus!
Just [create a new layout](../customization/customization-helper#h-22-layouts) for it!

# 3. Managing Custom GUIs
You can **open** and **delete** your custom GUIs in the [Custom GUIs tab](../customization/customization-helper#h-3-managing-custom-guis) of the [Customization Helper](../customization/customization-helper).

# 4. Using Custom GUIs
There are currently two ways to use custom GUIs.

The first one is using the [`opencustomgui`](../customization/custom-buttons#opencustomgui) button action of [custom buttons](../customization/custom-buttons).
This allows you to open a custom GUI by clicking a button.

The second one is overriding an existing menu with your custom GUI.
This is not recommended and should only be done when there is no way to [edit a menu using layouts](../customization/customization-helper).