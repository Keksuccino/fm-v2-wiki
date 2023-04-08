---
title: FAQ
description: Frequently asked questions about FancyMenu.
published: true
date: 2022-07-12T18:15:05.587Z
tags: misc
editor: markdown
dateCreated: 2021-12-22T00:43:13.299Z
---

# About
Here you can find frequently asked questions about FancyMenu.
Please read this before asking anything.

# Frequently Asked Questions
<br>

## What is FancyMenu?
FancyMenu is a Minecraft mod to [customize](./customization/layout-editor) the look and feel of menus in the game, like adding new elements to menus and edit existing elements like buttons.

## How to get rid of the customization buttons at the top of menus?
You can toggle its visibility by pressing **CTRL + ALT + C** (by default; changeable in MC settings) or by disabling them in the mod settings.

## How can I customize menus?
If you're new to FancyMenu, please take a look at the [wiki](http://fm.keksuccino.de).
It will help you to understand how FancyMenu works and how to make your menus awesome!

## What does term X mean?
If you don't know what's the meaning of one of FancyMenu's special terms, you can check out the [FancyMenu Slang](./fancymenu-slang) page.

## Can I use FancyMenu in my modpack?
**Yes**! You can freely use FancyMenu without any special requirements!

## Why is my WAV audio not working?
There are 4 things that could cause your audio to not play correctly:

### 1. The audio is not compatible with the mod.
Please be sure that your audio:

- Has a sample rate of 48KHz
- Has a bit rate of 16bit
- Is a valid **WAV** file that works outside of MC

You can easily (re)convert your audio to the correct bit and sample rate by using [this website](https://audio.online-convert.com/convert-to-wav).

> **IMPORTANT**: If you think your audio already has the correct format, bit rate and sample rate, please re-convert it anyway using the website mentioned above.
{.is-warning}

### 2. Your volume is too low.

Maybe your MC master volume is too low for you to hear the audio.

### 3. One of your other mods is incompatible with FancyMenu and causes audio issues.

In that case, please [open an issue](https://github.com/Keksuccino/FancyMenu/issues) on GitHub.

### 4. A world is loaded (you're in-game) while trying to play menu audios.

By default, FancyMenu doesn't play menu **background** audios while in a world.
That's because world background music could overlap with your menu audios when both are being played.
To change this, just enable **Custom Sounds In World** in the FancyMenu settings.

## Why is my OGG audio not working?
If your OGG audios won't start and maybe spamming errors to your log, there's probably something wrong with them.

They will probably work when you play them in a normal audio player, but Minecraft is a bit more picky than a "normal" player.

### Fixing the Audio
90% of your audio file problems get solved by simply re-converting them.

1. Go to https://convertio.co/ogg-mp3/ and convert your OGG to MP3.
2. Go to https://convertio.co/mp3-ogg/ and convert the MP3 (you got from the last step) back to OGG.

The file should work fine now!

## Resizing the Minecraft window or changing the scale makes my layout look weird, what can I do?
You're probably using the [wrong orientations](./customization/orientations) for your elements.

## What's a good place to ask for help about FancyMenu?
I'm very active in [discord](http://discord.keksuccino.de) and will give my best to help you with your problem!

## Menus of another mod are acting weird with FancyMenu installed, what can I do?
This means, the other mod is not fully compatible with FancyMenu.
In this case, please [disable customizations](./customization/customization-helper#h-21-customization-onoff) for this menu.

## The mod is crashing my game! What's wrong?
I'm sorry to hear that! I always try to make FancyMenu as stable as possible, but if you encounter an error or crash, please [open a bug report ticket](https://github.com/Keksuccino/FancyMenu/issues) with detailed informations about what happened and I will give my best to help you and fix the bug!

**If using other mods:**
One of your other mods could be incompatible with FancyMenu, so please don't forget to check out the [list of incompatible mods](./incompatibility-list) too!

## I have a nice idea, how can I suggest it to you?
That's great! If you have an idea for FancyMenu, please [open a feature request](https://github.com/Keksuccino/FancyMenu/issues)!

## Where can I share my cool menu with the community?
You can share your creations in [r/fancymenu](https://www.reddit.com/r/FancyMenu/) or via [discord](http://discord.keksuccino.de)!

## Will you backport the mod to MC version X?
It's possible that I backport FancyMenu to more older versions in the future, but asking me will not make the porting-process any faster.
You will know it when you see the download on the CurseForge page.

## Why isn't it possible to remove the mojang copyright text in the main menu?
I will not touch copyright notices for obvious reasons.

You can change its position via the [FancyMenu settings](./mod-settings), but it's not possible to remove it.

## The menu I want to edit doesn't show my customizations, what's wrong?
If customizations or config options does not affect a menu, it is possible that a mod is overriding the specific menu, which could make it incompatible with FancyMenu. In that case, check the menu identifier of the menu (you can find it by clicking on the "Menu Info" button) and [open a bug report ticket](https://github.com/Keksuccino/FancyMenu/issues) with your problem. Please include the menu identifier in your report. Thank you!

## Where can I check if my other mods are compatible with FancyMenu?
There is a [list of incompatible mods](./incompatibility-list) in the wiki you can check out!
Of course, this list is not completed, but it's a good start to find why something is not working as expected!

## Why can't I customize buttons of Optifine menus?
Optifine menus are not fully supported by FancyMenu. You can use all customization actions on these menus, but button modifications are disabled because this would break the menu's functionality.

This also includes the video settings menu when Optifine is installed, because Optifine overrides this menu.