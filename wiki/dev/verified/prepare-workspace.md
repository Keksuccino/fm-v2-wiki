---
title: Prepare Workspace
description: First steps for using the FancyMenu API.
published: true
date: 2023-02-10T22:47:15.220Z
tags: api
editor: markdown
dateCreated: 2023-02-10T22:47:13.900Z
---

# 0. About
To be able to write extension mods for FancyMenu, you will first need to prepare your workspace for it.

# 1. The Dependencies
Every FM extension mod depends on two other mods: [FancyMenu](https://github.com/Keksuccino/FancyMenu) and [Konkrete](https://github.com/Keksuccino/Konkrete).

## 1.1. The `mods.toml` File
You need to add at least FancyMenu to the mod dependencies of your `mods.toml` file.

Just add this section at the bottom of your `mods.toml` file and replace `your_mod_id` with the actual mod ID of your mod:
```
[[dependencies.your_mod_id]]
modId="fancymenu"
mandatory=true
ordering="AFTER"
versionRange="[2.3.6,)"
side="CLIENT"
```

## 1.2. Workspace
You need to include deobfuscated builds of FancyMenu and Konkrete as libraries in your workspace.
You can compile the sources by yourself using the **GitHub pages** of [FancyMenu](https://github.com/Keksuccino/FancyMenu) and [Konkrete](https://github.com/Keksuccino/Konkrete), or you just use the dev builds on the CurseForge pages of both mods.
These dev builds are uploaded as **additional file** for every normal build.
You can identify dev builds by the the name prefix `dev_`.

![](https://user-images.githubusercontent.com/35544624/141366573-b8b2f776-c519-4816-87e8-6b9b8e38358f.png)

## 1.3. The `run` Directory
It's needed for some mod loader/MC versions to add dependency mods to the `mods` directory of your IDEs `run` directory.

If you're getting a missing mod error when starting your IDEs' MC instance, just add the mods to the `mods` dir.

# 2. Verifying The Dependencies
After adding all dependencies, try to call `CustomizationItemRegistry.registerItem()` to see if everything works correctly.

If your workspace finds the class, you're done and can start writing fancy extension mods!