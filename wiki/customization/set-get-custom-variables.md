---
title: Set/Get Custom Variables
description: Set variables via buttons and sliders and use them in visibility requirements and placeholders!
published: true
date: 2022-11-29T22:43:10.767Z
tags: guide
editor: markdown
dateCreated: 2022-11-29T22:26:00.464Z
---

# 0. About

This guide will show you how to use custom variables in FancyMenu to use them in visibility requirements and placeholders.

# 1. Understanding the Basics

Custom variables in FancyMenu are variables that can be created and handled by layouts.

Variables are always stored a strings, so you can save basically everything to them, you just need to know how to handle it later.

# 2. Creating, Setting and Using Variables in Layouts

There are multiple ways to set and get values in layouts.

> You need to input a **variable name** in multiple places when working with variables.
This variable name needs to be **unique**, so keep that in mind when creating a variable.
It's basically the identifier of your variable and you need it to get the variable value later, so don't forget it!
{.is-warning}

## 2.1. Creating and Setting
Creating a new variable is pretty easy and happens semi-automatic.

There are currently three ways to set (and create) a variable value via layouts.

### 2.1.1. Custom Buttons
The first one is by using a **custom button** with the `set_variable` button action.
If you set a variable that doesn't exists yet, it will be created automatically.

### 2.1.2. Sliders
The second way is by using a **slider element**.
These elementy are specifically for setting variables, so you can't do other things with it.
Similar to buttons, non-existant values will be automatically created when setting them via the slider.

### 2.1.3. Text Input Fields
The third one is by using a **text input field element**.
These are basically text boxes. Similar to sliders, these elements only set variables and non-existant variables will be automatically created when setting them.

## 2.2. Using
Variables can be used in the **Is Variable Value** visibility requirement (to hide/show elements/layouts depending on the variable value) and in the **Get Variable** placeholder (to display the variable value). 

# 3. Using a Command to Manage Variables
There is a command (`/fmvariable`) to create, set, get and remove variables.
This command can be used for debugging and to let other mods like **FTB Quests** set variables.
