---
title: Panoramas
description: Create panoramas and use them as menu background.
published: true
date: 2023-02-10T22:47:38.819Z
tags: customization
editor: markdown
dateCreated: 2023-02-10T22:47:37.579Z
---

# 0. About

As of v1.6.0, FancyMenu supports loading custom 6-image panorama cubes as background for menus!

> **NOTE**: "6-image panoramas" are a special cubic panorama format used by Minecraft as background in the main menu.
{.is-info}

> **IMPORTANT**: If you're on Windows, don't forget to turn on [file extensions](https://cdn.discordapp.com/attachments/795308330746511390/801561308012347482/unknown.png)!
{.is-warning}

# 1. Making a Panorama

If you don't know how Minecraft handles their background panoramas and how to create these, you should check out [this video](https://www.youtube.com/watch?v=F7jMd3zsjZQ&t).
It will give you a very good understanding of how MC panoramas work and how to make one!

After watching the video, you will notice that creating MC panoramas can be a bit time-consuming.
To save you some time, maybe think about using a mod that creates these panoramas for you.
You can find some of them by searching for `minecraft panorama mod`, but one of them is [Panoramica](https://www.curseforge.com/minecraft/mc-mods/panoramica) (made by me).

# 2. Preparing The Panorama

After you got your 6 panorama images, you'll need to put them at the right place!

FancyMenu's panorama directory is located at `.minecraft/config/fancymenu/panoramas`.
This is the directory for all panoramas that you want to use in the mod.

## 2.1. The Panorama Folder

Every panorama has its own folder.
You will need to create a new folder in `.minecraft/config/fancymenu/panoramas` if you want to add a new panorama.
In my example, I will name the folder `mypanorama`.

![1](https://user-images.githubusercontent.com/35544624/100791916-2802d380-341a-11eb-8e32-f9913e93a38c.png)

## 2.2. Folder Content

After creating the folder, you will need to fill it.

### 2.2.1. Properties File
Every panorama needs a properties file to work.
This file always needs to be named `properties.txt` and needs some important things written to it.

The content of a panorama properties file should always look like this:
```
type = panorama

panorama-meta {
  name = name_of_your_panorama
  speed = 1.0
  fov = 85.0
  angle = 25.0
}
```
Only the variables inside the `panorama-meta` section can be changed!

#### name
This has to be the **unique** name of your panorama.
It's not possible to load two panoramas with the same name!
You will use this name later to identify your panorama.

#### speed
The speed at which your panorama rotates.
This value is a speed multiplicator. For example, `1.0` is default speed, `2.0` doubles the speed and `0.5` will half it.
Negative values are not supported, use decimal values to slow the speed.

#### fov
The field of view.
The default FOV is `85.0`.
Using too big or small values here will break the panorama. Just play around with it to find the FOV you want.

#### angle
The vertical angle at which the panorama is viewed.
The default angle is `25.0`.

### 2.2.2. Panorama Image Folder

The second mandatory thing your panorama folder needs is the actual image folder containing your panorama images.

This folder needs to be named just `panorama`.

Put all your panorama frames in it, but don't forget to name them correctly like shown in the [video](https://www.youtube.com/watch?v=F7jMd3zsjZQ&t) above!

![3](https://user-images.githubusercontent.com/35544624/100791922-29340080-341a-11eb-8174-874a180d0485.png)

> **NOTE:** Only PNGs are supported as panorama images!
{.is-info}

### 2.2.3. Panorama Overlay

The last step is **optional** and can be skipped if you don't want an overlay over your panorama.

If you want to add a vignette or other types of overlays to your panorama, you can add one named 'overlay.png'.
Keep in mind that only PNG is supported for the overlay and that the file name always needs to be 'overlay.png'!

### 2.2.4. The Final Product

You should now have a folder located at `.minecraft/config/fancymenu/panoramas`, containing a `properties.txt` file, another folder named `panorama` and maybe an overlay named `overlay.png`.

![2](https://user-images.githubusercontent.com/35544624/100791920-29340080-341a-11eb-8e26-98a7fd2ad7eb.png)

# 3. Using The Panorama

After reloading the game via the [Reload button](./customization-helper#h-1-the-reload-button) or restarting it, you should be able to use your panorama in the [Layout Editor](./layout-editor) (Background Options).