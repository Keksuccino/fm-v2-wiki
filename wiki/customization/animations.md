---
title: Animations
description: Use animations as menu background and more.
published: true
date: 2023-02-10T22:47:19.371Z
tags: customization
editor: markdown
dateCreated: 2023-02-10T22:47:18.106Z
---

# 0. About

You can make your own animations and show them as menu backgrounds or gif-like animations in menus.

*Just think about all the memes you can put in menus with this!*

> **IMPORTANT**: If you're on Windows, don't forget to turn on [file extensions](https://cdn.discordapp.com/attachments/795308330746511390/801561308012347482/unknown.png)!
{.is-warning}

# 1. Getting started

Making animations is really easy.

Most of the work is done by a neat little tool, the [Animation Maker](https://www.curseforge.com/minecraft/mc-mods/fancymenu-animation-maker-tool).
This tool will do all the annoying stuff for you, like writing properties files for your animation.
It will pack your animation to an animation pack, ready for you to copy it to the Minecraft directory.

# 2. Preparing the Animation Frames
You need to know, animations are just a bundle of many image files (or frames).
They get quickly shown, or played, one by the other.

> **NOTE**: If you already have your animation separated into its frames and the frames are valid **JPG/JPEG** or **PNG** files, you can skip this step and continue with **step 3**.
{.is-info}

If you only have a video file and you want to use this video as animation, you need to split your video into its frames first.

There are plenty of tools to export frames from video files, like **Adobe Premiere Pro** or other similar video editing softwares, but you can also use **free online services** for this.
One of these online services is [OnlineConverter.com](https://www.onlineconverter.com/video-to-jpg).

Just upload your video to the OnlineConverter website (max. 200MB file size) and export it as JPG images.

> **WARNING**: Loading animation frames in Minecraft can **consume a lot of memory**!
Try to not use more than **200 total frames** per animation at a maximum resolution of **1920x1080**!
{.is-warning}

Now you have a ZIP with lots of image files. Unpack these image files to an empty folder and you're done with preparing your frames.

# 3. Packing the Animation

Now you have your animation frames, but they are..well..just lots and lots of images at the moment.
Let's change that!

Remember the tool mentioned above? Now's the [Animation Maker](https://www.curseforge.com/minecraft/mc-mods/fancymenu-animation-maker-tool)'s time to shine!

Download the tool to your PC and open it by **double-clicking** the **JAR** file.
**Don't confuse it with a Minecraft mod! It's a standalone tool!**

Now you should see a window with lots of things to configure.

<img src="https://user-images.githubusercontent.com/35544624/136706643-5b7b68c3-b25d-4d8f-9bd4-01ba39051675.png" alt="Animation Maker" width="250"><br>

This window will let you configure and export your animation pack.

It's recommended to fill all input fields from top to down:

## 3.1. Unique Animation Identifier
This is the **unique** name, or identifier, of your animation.

It's really important that this identifier is **as unique as possible**, so it's recommended to just start with a unique character combination only you're using, like your username and a bunch of numbers as ID.

A good and unique animation identifier can look like this:
`keksuccino_9832498_mycoolanimation`

> **And for gods sake, please don't use the example identifier for your own animation!**
{.is-warning}

## 3.2. Animation FPS
This value is the amount of **Frames Per Second** your animation is played at.

The most **recommended** value for smooth and good looking animations is **24 FPS**, but keep in mind that it's not enough to just set the FPS value here. **Your animation obviously needs to work with the same FPS!**

## 3.3. Main Animation
This section contains everything related to your the main/base animation of your pack.
The main animation is just the "normal" animation part that every animation pack needs.
This is where the frames you've prepared in **Step 1** will be used.

### 3.3.1. Loop Animation
If your animation should be looped like a GIF or if you only want to play it one single time.

### 3.3.2. Animation Audio (Optional)
This audio is played as background audio for the **main** animation.

The **audio gets looped with the animation**! If the animation is restarting, your audio will too!
It's not recommended to use songs here, it's more like a way to add some simple background sounds like rain sounds, birds, etc.

### 3.3.3. Animation Frames
Finally! Here you can add the actual animation frames to your main animation.

Click the **Add Frames** button and add all the animation frames you've prepared in **Step 1**.
**Frames will later be played in the same order they're ordered in this list.**

![Screenshot_3](https://user-images.githubusercontent.com/35544624/136706645-d4260f07-5ded-446d-90e5-03d547167fc2.png)

> **NOTE**: If you add multiple files at once, they will be ordered alphabetically and by numbers.
{.is-info}

## 3.4. Intro Animation (Optional)
This section is optional!

Animation intros are separate animations that will be played before the main animation starts.

Intro animations are **not being looped with the main animation**, they are just played one time when the animations gets shown and then the main animation starts playing and looping, if enabled.

This allows you to play more advanced animations with some different frames at the beginning before the main animation starts looping.

Most parts of this section are exactly the same as the **Main Animation** section, so please just do the same as described there.

### 3.4.1. Replay Intro
The only option that's different here is the **Replay Intro** option.

Here you can configure if your intro animation should be played (replayed) every time the animation is shown (like when you have your animation in menu A, go to menu B and the animation is replayed when going back to menu A) or if you just want to play the animation the **very first time** it gets shown an then never again.

## 3.5. Save To
Well, pretty obvious, right?
You did it! You're ready to export your animation pack now!

Save it to your desktop or another location you can easily remeber.

# 4. Installing 'Load My Resources'
[Load My Resources](https://www.curseforge.com/minecraft/mc-mods/load-my-resources-forge) is a mod to easily load resources like images and sounds automatically on game start. It's like a resource pack, but it's enabled by default and can't be disabled by the user.

You need this mod to load the frames of the animation.

Download the mod from [CurseForge](https://www.curseforge.com/minecraft/mc-mods/load-my-resources-forge) and install it in your Minecraft instance.

# 5. Importing the Animation to Minecraft
You're nearly done, just a few easy things left.

Go to the location you've exported your animation pack to (via the [Animation Maker](https://www.curseforge.com/minecraft/mc-mods/fancymenu-animation-maker-tool)) and locate the animation pack folder. It should have the same name as the **animation identifier** you've set in the [Animation Maker](https://www.curseforge.com/minecraft/mc-mods/fancymenu-animation-maker-tool).

Open the animation pack folder, locate the `COPY_CONTENT_TO_MINECRAFT_FOLDER` folder and go into it.

Here you should have two folders, one called `config` and another one called `resources`.

Copy these two folders to your Minecraft instance directory (`.minecraft`).
If you don't know how to find the `.minecraft` folder, take a look at [this page](https://minecraft.fandom.com/wiki/.minecraft).

> **Don't delete the already existing `config` and `resources` folders in `.minecraft`!
Just copy the folders of the animation into `.minecraft`, so the folder contents get merged.**
{.is-warning}

# 6. Enabling and Using the Animation Pack
Last step, I promise!

After you've copied the animation pack to your `.minecraft` folder, just (re-)start Minecraft and you're done!

Congrats! Now you're ready to use the animation as animation element or background animation for your menus in the [Layout Editor](./layout-editor)!