---
title: Include Layouts in Modpacks
description: Guide about how to ship menu layouts with modpacks.
published: true
date: 2023-02-18T23:29:05.052Z
tags: guide, layout, modpack, export, setup, ship, include
editor: markdown
dateCreated: 2022-05-08T00:39:53.183Z
---

# 0. About

This guide will focus on how to ship FancyMenu setups with modpacks.

# 1. Adding Setups to Modpacks

Before you can start, you will first need to [export your FancyMenu setup](./share-setups#h-1-export-setups).

After you've exported the setup, open the folder of the setup and search for the `setup` folder.

![Screenshot_10](https://user-images.githubusercontent.com/35544624/167276523-1f7d569e-0901-4d73-8a93-0f9bf99acbf9.png)

Inside of the `setup` folder is every part of your Minecraft instance that is in some way related to your FancyMenu setup.
This is everything starting from config files to layouts, layout resources, animations and so on.

Since the `setup` folder is basically just the Minecraft instance (`.minecraft` by default), but without everything that's not related to FancyMenu, you can just **copy** the content of the `setup` folder to the root directory of your modpack instance (that's the `overrides` folder for CurseForge packs) and you're done.

> Keep in mind that, depending on what platform you're using for your modpack, you will need to **manually include custom files and folders** that don't get uploaded with your pack by default.
{.is-warning}

# 2. Hiding the FancyMenu Overlay by Default

> The FancyMenu overlay is the menu bar at the top of menus and the Drippy Loading Screen button if you have that installed.
{.is-info}

To manually hide the overlay for a setup you exported, navigate to `setup/config/fancymenu/` in the folder of the exported FancyMenu setup, search for the `config.txt` file and open it in a text editor.

Now search for `showcustomizationbuttons` and set it to `false`.

![Screenshot_1](https://user-images.githubusercontent.com/35544624/219902703-4eda7629-3612-4d1f-b508-7032fa8ddf55.png)

That's basically it. Save the file and now the overlay should be completely hidden when you launch the modpack.