---
title: Customization Helper
description: The menu bar at the top of every menu. Used to access all mod features.
published: true
date: 2023-02-10T22:47:27.060Z
tags: tools, customization
editor: markdown
dateCreated: 2023-02-10T22:47:25.786Z
---

# 0. About
Maybe you've already discovered the weird menu bar in all your Minecraft GUIs.
This is the Customization Helper. It contains everything you need to customize your menus.

Most of the tabs in this bar are focussing on the current menu you see.
You can create layouts for the current menu there, get informations about the menu and more, but the Customization Helper also contains some stuff that's not related to the current menu, like creating and managing custom GUIs.

![1](https://user-images.githubusercontent.com/35544624/111196670-d5f74f80-85bd-11eb-9c7e-a9f06434c516.png)

# 1. The Reload Button
The little curved/spinning arrow button on the right side is the reload button.

![reload](https://user-images.githubusercontent.com/35544624/111198211-9a5d8500-85bf-11eb-93c8-8955653fb2e3.png)

This button reloads much things that FancyMenu caches, like layout files, the [mod settings](../mod-settings), [panoramas](./panoramas), [slideshows](./slideshows) and [button scripts](../advanced/button-scripts).

It does **not** apply changes made to [animations](./animations).
You need to **restart** your game after changing or creating animations.

# 2. Customizing Menus
The **Current Menu** tab contains stuff to customize the menu you see.

![current-menu](https://user-images.githubusercontent.com/35544624/111200593-3a1c1280-85c2-11eb-9c4e-6ef65327c417.png)

## 2.1. Customization On/Off
The first option in this tab toggles the customization system for the **current** menu (not for all menus).
By default, the customization system is disabled for all menus and will not show any layouts and customizations you apply to a menu.

To change this, simply switch this option to **On** by leftclicking it.

![customization-on-off](https://user-images.githubusercontent.com/35544624/111200785-5fa91c00-85c2-11eb-812f-22d422832787.png)

## 2.2. Layouts
This option allows you to create and manage [layouts](../fancymenu-slang) for the current menu.
With layouts, you can completely customize the look and feel of menus by using the [Layout Editor](./layout-editor).

![layouts](https://user-images.githubusercontent.com/35544624/111201345-f675d880-85c2-11eb-8eb5-69b5a92c5ff4.png)

## 2.3. Advanced
The last option in this tab contains things for **advanced users**.
You can **override** the current menu with one of your [custom GUIs](../advanced/custom-guis) here.

You need to enable the **Advanced Mode** in the [FancyMenu Settings](../mod-settings) to enable this tab!

> **OVERRIDING A MENU IS NOT RECOMMENDED AND SHOULD ONLY BE DONE IF YOU CAN'T EDIT IT USING A LAYOUT!**
{.is-warning}

![advanced](https://user-images.githubusercontent.com/35544624/111202124-d1359a00-85c3-11eb-879f-df416a269e37.png)

# 3. Managing Custom GUIs
The **Custom GUIs** tab contains everything you need to create and manage your [custom GUIs](../advanced/custom-guis).

![custom-guis](https://user-images.githubusercontent.com/35544624/111202782-8ff1ba00-85c4-11eb-8683-ee6307ff4013.png)

Well, there's not really much to say about this tab.
You can open [custom GUIs](../advanced/custom-guis) with [custom buttons](./custom-buttons). This is the recommended way to use them.
Please **be careful** when overriding a menu with a custom GUI. This should only be done when you really can't edit the menu using a [layout](../fancymenu-slang#layout).

You need to enable the **Advanced Mode** in the [FancyMenu Settings](../mod-settings) to enable this tab!

# 4. Get Informations about Menus
The **Tools** tab contains useful tools to get informations about the current menu.

![tools](https://user-images.githubusercontent.com/35544624/111203573-7ac95b00-85c5-11eb-8e8e-7740ee2bc62f.png)

## 4.1. Menu Info
This feature will show you the [menu identifier](../fancymenu-slang#menu-identifier) for the current menu in the upper-left corner.
This identifier is important when you want to open a menu by using a [custom button](./custom-buttons) and other things.

![menu-info](https://user-images.githubusercontent.com/35544624/111203871-cda31280-85c5-11eb-9f37-8577fcedf9d9.png)

> **NOTE:** You can **left-click** the menu identifier to copy it to your clipboard.
{.is-info}

## 4.2. Button Info
This one, when activated by clicking on it, will show you informations about a **vanilla** button, when you hover over it. (Doesn't work for [custom buttons](./custom-buttons))

![button-info](https://user-images.githubusercontent.com/35544624/111204479-73ef1800-85c6-11eb-9822-361e1ca0b76d.png)

It's basically a debug tools to check things like the button size and positon without needing to open the [Layout Editor](./layout-editor).

# 5. Other Useful Stuff
The **Miscellaneous** tab contains everything that doesn't really fit in a category.
For now, you can force-close menus with it and **open "dead" instances of some menus** that you normally can't customize, because they disappear to fast, like the **world loading screen**.

![misc](https://user-images.githubusercontent.com/35544624/111205267-58d0d800-85c7-11eb-9fd0-7cb186c8d5a1.png)

> **NOTE:** This tab maybe looks different for you, because it doesn't have the same content in all MC versions.
{.is-info}