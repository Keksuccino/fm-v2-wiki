---
title: Custom Button Actions
description: Create custom button actions that can be executed on button click using the FancyMenu API.
published: true
date: 2023-02-10T22:47:05.620Z
tags: api
editor: markdown
dateCreated: 2023-02-10T22:47:04.298Z
---

# 0. About
The FancyMenu API allows you to add your own custom button actions via an extension mod. These button actions can be used for [custom button elements](../customization/custom-buttons) and will be executed on button click.

# 1. Preparing Your Workspace
To prepare your workspace for the FancyMenu API, please take a look at the [Preparing The Workspace](./prepare-workspace) wiki page.

# 2. Adding New Button Actions
Every custom button action needs to be wrapped into a [`ButtonActionContainer`](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/buttonaction/ButtonActionContainer.java).
This container needs to be registered to the [`ButtonActionRegistry`](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/buttonaction/ButtonActionRegistry.java) on mod init.

## 2.1. Creating the Button Action Container

Create a new subclass of [`ButtonActionContainer`](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/buttonaction/ButtonActionContainer.java) for your button action and give it a fitting name.
In this case, I will name my example button action class `ExampleButtonActionContainerWithValue`.

There are some important things in this class that need a bit of explaination.

### 2.1.1. The Constructor
The constructor is used to set the **unique** identifier of your button action.
This identifier needs to be **unique**! It isn't possible to register two actions with the same identifier!
The identifier is not your actual button action name, so you can choose a very unique string here.
It's recommended to use **something unique as prefix, like your username**. Otherwise it could conflict with other extension mods.

```java
    public ExampleButtonActionContainerWithValue() {
        //The action identifier needs to be unique, so just use your username or something similar as prefix
        super("super_unique_action_identifier");
    }
```

### 2.1.2. The `getAction()` Method
This method returns the actual name of your action.
This name is used in the editor, so choose a fancy one!
It should fit with what your action does.

```java
//The name of your action. Should be lowercase and without any spaces.
@Override
public String getAction() {
    return "customaction";
}
```

### 2.1.3. The `hasValue()` Method
Here you can set if your button action has a value or not.
For example, the [`opengui`](../customization/custom-buttons#opengui) button action has the menu identifier as value.
On the other hand, there's the [`closegui`](../customization/custom-buttons#closegui) button action, which doesn't has a value, because it doesn't need one.

```java
//If the custom action has a value or not
@Override
public boolean hasValue() {
    return true;
}
```

### 2.1.4. The `execute(..)` Method
The most important method in this class.
This method is basically your button action body.
It will be called when a custom button with this button action is getting clicked.

It has the button action value as parameter.
This **parameter can be null**, so take care of that.

Everything your button action should do on button click needs to be handled in this method.

```java
//Gets called when a button with this custom action is getting clicked
@Override
public void execute(String value) {

    //This will open a new instance of the dirt message screen, when a button with this custom action is getting clicked
    //and will show the action value as message
    if (value != null) {
        Minecraft.getInstance().setScreen(new GenericDirtMessageScreen(new TextComponent(value)));
    }

}
```

### 2.1.5. The `getActionDescription()` Method
This is the description of your button action.
It will be shown in the layout editor.

> **IMPORTANT:** Needs to be **as short as possible**, because the button action selection screen does not has much space for it.
{.is-warning}

```java
//The description of the action
@Override
public String getActionDescription() {
    return "Show custom text in a dirt message screen.";
}
```

### 2.1.6. The `getValueDescription()` Method
This is the description of your button action **value**.
If your button action has a value, you maybe want to describe a bit what exactly it is.
The value description is actually more like a type description.

> If your button action does not has a value, just return **null** here.
{.is-info}

> **IMPORTANT:** Needs to be **as short as possible**, because the button action selection screen does not has much space for it.
{.is-warning}

```java
//The action has a value, so I return a simple and short value description here.
//This is actually more like a value type description.
@Override
public String getValueDescription() {
    return "Display Text";
}
```

### 2.1.7. The `getValueExample()` Method
That method returns an example of how the action value of your button action should look like.

> If your button action does not has a value, just return **null** here.
{.is-info}

> **IMPORTANT:** Needs to be **as short as possible**, because the button action selection screen does not has much space for it.
{.is-warning}

```java
//That's an example of how the action value should look like.
@Override
public String getValueExample() {
    //Well, it's just a simple String, so what should be the example here >.<
    return "cool text to display";
}
```

### 2.1.8. Full Example
Here is a full working [`ButtonActionContainer`](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/buttonaction/ButtonActionContainer.java) example.

```java
package de.keksuccino.fancymenu.api.buttonaction.example;

import de.keksuccino.fancymenu.api.buttonaction.ButtonActionContainer;
import net.minecraft.client.Minecraft;
import net.minecraft.client.gui.screens.GenericDirtMessageScreen;
import net.minecraft.network.chat.TextComponent;

public class ExampleButtonActionContainerWithValue extends ButtonActionContainer {

    public ExampleButtonActionContainerWithValue() {
        //The action identifier needs to be unique, so just use your username or something similar as prefix
        super("super_unique_action_identifier");
    }

    //The name of your action. Should be lowercase and without any spaces.
    @Override
    public String getAction() {
        return "customaction";
    }

    //If the custom action has a value or not
    @Override
    public boolean hasValue() {
        return true;
    }

    //Gets called when a button with this custom action is getting clicked
    @Override
    public void execute(String value) {

        //This will open a new instance of the dirt message screen, when a button with this custom action is getting clicked
        //and will show the action value as message
        if (value != null) {
            Minecraft.getInstance().setScreen(new GenericDirtMessageScreen(new TextComponent(value)));
        }

    }

    //The description of the action
    @Override
    public String getActionDescription() {
        return "Show custom text in a dirt message screen.";
    }

    //The action has a value, so I return a simple and short value description here.
    //This is actually more like a value type description.
    @Override
    public String getValueDescription() {
        return "Display Text";
    }

    //That's an example of how the action value should look like.
    @Override
    public String getValueExample() {
        //Well, it's just a simple String, so what should be the example here >.<
        return "cool text to display";
    }

}
```

## 2.2. Registering The Container
You're almost done! Just one last, important step.

FancyMenu needs to know about your custom button action, so you need to register your [`ButtonActionContainer`](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/buttonaction/ButtonActionContainer.java) to the [`ButtonActionRegistry`](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/buttonaction/ButtonActionRegistry.java) when your extension mod gets initialized.

```java
package de.keksuccino.fancymenu;

import net.minecraftforge.fml.common.Mod;
import de.keksuccino.fancymenu.api.buttonaction.ButtonActionRegistry;

@Mod("modid")
public class ExampleModMainClass {

    public ExampleModMainClass() {
        try {

            //Register your ButtonActionContainer to the ButtonActionRegistry at mod init.
            ButtonActionRegistry.registerButtonAction(new ExampleButtonActionContainerWithValue());

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

Now you can use your own button action for [custom buttons](../customization/custom-buttons)!