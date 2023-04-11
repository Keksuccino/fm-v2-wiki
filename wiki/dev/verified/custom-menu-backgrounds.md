---
title: [DEV] Custom Menu Backgrounds
description: Create custom menu backgrounds using the FancyMenu API.
published: true
date: 2023-04-11T01:19:35.514Z
tags: api
editor: markdown
dateCreated: 2023-04-07T04:32:25.712Z
---

# 0. About
The FancyMenu API allows you to add your own custom menu backgrounds via an extension mod, so you can use them in layouts.

> **IMPORTANT**: The Menu Background API is only available in FancyMenu v2.6.2+ !
{.is-warning}

# 1. Preparing Your Workspace
To prepare your workspace for the FancyMenu API, please take a look at the [Preparing The Workspace](./prepare-workspace) wiki page.

# 2. Adding Menu Backgrounds
Every menu background needs two classes to work.

The first one is the [MenuBackgroundType](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackgroundType.java).
This is the type of your background (like the already existing animation and panorama background types).

The second one is [MenuBackground](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackground.java).
This class is an instance of your menu background. [MenuBackgroundType](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackgroundType.java)s hold and create [MenuBackground](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackground.java)s, so they can be rendered in layouts.

Every [MenuBackgroundType](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackgroundType.java) needs to be registered to the [MenuBackgroundTypeRegistry](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackgroundTypeRegistry.java) at mod init.

## 2.1. Different Kinds of Backgrounds
It's important to mention that there are basically two kinds of menu backgrounds.
The first one (**normal mode**) initializes a set of [MenuBackground](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackground.java) instances at mod start, so the user can choose from this set of backgrounds.

The second one (**input string mode**) has no instances to choose from, but takes an input string to create a new instance.
This input string has basically no limitations. It can be a simple file path or a 10000 char long string to build an instance.
The user has the ability to click on an "input string button" to enter the input string.
This button is fully customizable, so you can open every type of configuration menu you want.

## 2.2. Creating a NORMAL (Non-Input-String) Background

Normal [MenuBackgroundType](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackgroundType.java)s initialize a set of [MenuBackground](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackground.java) instances at game start for the user to choose from.

### 2.2.1. The `MenuBackground` Class

Create a new subclass of the [MenuBackground](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackground.java) class and give it a fitting name.
In this case, I will name my example class `ExampleMenuBackground`.

There are some important things to take care of here.

#### 2.2.1.1. The Constructor
The constructor is where you define the **unique** identifier of your background.
It can also be used to set variables on construction.

```java
public ExampleMenuBackground(@Nonnull String uniqueBackgroundIdentifier, @Nonnull MenuBackgroundType type, Color color) {
    //The identifier needs to be UNIQUE!
    //It's not possible to register multiple backgrounds with the same identifier to the same background type.
    super(uniqueBackgroundIdentifier, type);
    //Custom color variable. Will get rendered as background later.
    this.color = color;
}
```

#### 2.2.1.2. The `onOpenMenu()` Method
This method gets called whenever a menu gets opened.
It doesn't get called every screen init (when resizing the window), but only when a menu gets opened (like when switching from menu A to menu B).

Use this method to reset stuff of your instance that should get reloaded when opening a new menu.

```java
@Override
public void onOpenMenu() {
    //Gets called when opening a NEW menu (not when resizing it).
    //If you want to reset stuff of your background instance when the menu changes, do it here.
}
```

#### 2.2.1.3. The `render()` Method
This method gets called to render your menu background instance.
Well, pretty self-explaining what to do here, right?

```java
//Here you will render the background instance.
//You should always render backgrounds over the full size of the screen, otherwise it will look ugly.
@Override
public void render(PoseStack matrix, Screen screen, boolean keepAspectRatio) {

    try {

        //Simply renders a colored background to the full size of the screen it is rendered in.
        //We will ignore the keepAspectRatio param here, because, well, a simple colored background has no aspect ratio.
        GuiComponent.fill(matrix, 0, 0, screen.width, screen.height, this.color.getRGB());

    } catch (Exception e) {
        e.printStackTrace();
    }

}
```

#### 2.2.1.4. Full Example Class

This is a full working [MenuBackground](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackground.java) example.

```java
package de.keksuccino.fancymenu.api.background.example.no_input_string;

import com.mojang.blaze3d.vertex.PoseStack;
import de.keksuccino.fancymenu.api.background.MenuBackground;
import de.keksuccino.fancymenu.api.background.MenuBackgroundType;
import net.minecraft.client.gui.GuiComponent;
import net.minecraft.client.gui.screens.Screen;

import javax.annotation.Nonnull;
import java.awt.*;

//This is an example menu background that simply renders a color.
//The color can be set on construction.
public class ExampleMenuBackground extends MenuBackground {

    protected Color color;

    public ExampleMenuBackground(@Nonnull String uniqueBackgroundIdentifier, @Nonnull MenuBackgroundType type, Color color) {
        //The identifier needs to be UNIQUE!
        //It's not possible to register multiple backgrounds with the same identifier to the same background type.
        super(uniqueBackgroundIdentifier, type);
        //Will get rendered as background.
        this.color = color;
    }

    @Override
    public void onOpenMenu() {
        //Gets called when opening a NEW menu (not when resizing it).
        //If you want to reset stuff of your background instance when the menu changes, do it here.
    }

    //Here you will render the background instance.
    //You should always render backgrounds over the full size of the screen, otherwise it will look ugly.
    @Override
    public void render(PoseStack matrix, Screen screen, boolean keepAspectRatio) {

        try {

            //Simply renders a colored background to the full size of the screen it is rendered in.
            //We will ignore the keepAspectRatio param here, because, well, a simple colored background has no aspect ratio.
            GuiComponent.fill(matrix, 0, 0, screen.width, screen.height, this.color.getRGB());

        } catch (Exception e) {
            e.printStackTrace();
        }

    }

}
```

### 2.2.2. The `MenuBackgroundType` Class

Create a new subclass of the [MenuBackgroundType](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackgroundType.java) class and give it a fitting name.
In this case, I will name my example background type class `ExampleMenuBackgroundType`.

There are some important things in this class you need to take care of.

#### 2.2.1.1. The Constructor
The constructor is used to set the **unique** identifier of your background type.

```java
public ExampleMenuBackgroundType() {
    //This identifier needs to be UNIQUE! It is not possible to register multiple types with the same identifier.
    super("example_type_no_input_string");
}
```

#### 2.2.2.2. The `loadBackgrounds()` Method
This method gets called to load or re-load the set of [MenuBackground](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackground.java) instances of the [MenuBackgroundType](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackgroundType.java).
The user can choose from this set of backgrounds.

```java
//In normal mode (when not using input strings), this is the place you register all of the background instances for the type.
//This method gets called on game start and when the reload button gets pressed.
//
//For example, when you want to use a directory where users can put their background properties, like FancyMenu does for animations and slideshows,
//load all backgrounds from this directory here.
@Override
public void loadBackgrounds() {

    //Clear the loaded backgrounds first.
    this.backgrounds.clear();

    //Background identifiers need to be UNIQUE when registering backgrounds!
    //It is not possible to register multiple backgrounds with the same identifier!
    //
    //In this case I just directly register a set of background instances,
    //but you can also use this (for example) to load stored background properties, etc.
    this.addBackground(new ExampleMenuBackground("green_background", this, new Color(117, 245, 66)));
    this.addBackground(new ExampleMenuBackground("blue_background", this, new Color(66, 126, 245)));
    this.addBackground(new ExampleMenuBackground("orange_background", this, new Color(245, 164, 51)));

}
```

#### 2.2.2.3. The `getDisplayName()` Method
Called to get the display name of the background type.
The display name is shown in the background options of the layout editor.

```java
//You don't really have much space for the display name, so try to choose a short one ond explain the type further in the description.
@Override
public String getDisplayName() {
    return "Example Type No Input";
}
```

#### 2.2.2.4. The `getDescription()` Method
Gets the description of the background type.
Shown in the background options of the layout editor.

```java
//Gets displayed when hovering over the type switcher in the background options menu in the layout editor.
//This is great for telling users everything important about your background type!
@Override
public List<String> getDescription() {
    List<String> l = new ArrayList<>();
    l.add("This background type has a set");
    l.add("of backgrounds to choose from.");
    l.add("It doesn't use input strings.");
    return l;
}
```

#### 2.2.2.5. The `needsInputString()` Method
This is one of the most important methods, because here you choose the mode of the background type.
In this case, we return `false` here, because we want the **normal mode** for our background type.

Returning `true` here would set the background type to the **input string mode**.

```java
@Override
public boolean needsInputString() {
    //Return false, because we don't use input strings for this type.
    return false;
}
```

#### 2.2.2.6. The `createInstanceFromInputString()` Method
This method is only used when the background type is set to the **input string mode**.
That's not the case here, so we just return `null`.

```java
@Override
public MenuBackground createInstanceFromInputString(String inputString) {
    //Return null, because we don't use input strings for this type.
    return null;
}
```

#### 2.2.2.7 Full Example Class
This is a full working [MenuBackgroundType](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackgroundType.java) example.

```java
package de.keksuccino.fancymenu.api.background.example.no_input_string;

import de.keksuccino.fancymenu.api.background.MenuBackground;
import de.keksuccino.fancymenu.api.background.MenuBackgroundType;

import java.awt.*;
import java.util.ArrayList;
import java.util.List;

//This is a background type that doesn't use an input string.
//It doesn't create background instances on-the-fly, but has a set of loaded instances to choose from.
public class ExampleMenuBackgroundType extends MenuBackgroundType {

    public ExampleMenuBackgroundType() {
        //This identifier needs to be UNIQUE! It is not possible to register multiple types with the same identifier.
        super("example_type_no_input_string");
    }

    //In normal mode (when not using input strings), this is the place you register all of the background instances for the type.
    //This method gets called on game start and when the reload button gets pressed.
    //
    //For example, when you want to use a directory where users can put their background properties, like FancyMenu does for animations and slideshows,
    //load all backgrounds from this directory here.
    @Override
    public void loadBackgrounds() {

        //Clear the loaded backgrounds first.
        this.backgrounds.clear();

        //Background identifiers need to be UNIQUE when registering backgrounds!
        //It is not possible to register multiple backgrounds with the same identifier!
        //
        //In this case I just directly register a set of background instances,
        //but you can also use this (for example) to load stored background properties, etc.
        this.addBackground(new ExampleMenuBackground("green_background", this, new Color(117, 245, 66)));
        this.addBackground(new ExampleMenuBackground("blue_background", this, new Color(66, 126, 245)));
        this.addBackground(new ExampleMenuBackground("orange_background", this, new Color(245, 164, 51)));

    }

    //You don't really have much space for the display name, so try to choose a short one ond explain the type further in the description.
    @Override
    public String getDisplayName() {
        return "Example Type No Input";
    }

    //Gets displayed when hovering over the type switcher in the background options menu in the layout editor.
    //This is great for telling users everything important about your background type!
    @Override
    public List<String> getDescription() {
        List<String> l = new ArrayList<>();
        l.add("This background type has a set");
        l.add("of backgrounds to choose from.");
        l.add("It doesn't use input strings.");
        return l;
    }

    @Override
    public boolean needsInputString() {
        //Return false, because we don't use input strings for this type.
        return false;
    }

    @Override
    public MenuBackground createInstanceFromInputString(String inputString) {
        //Return null, because we don't use input strings for this type.
        return null;
    }
}
```

### 2.2.3. Registering the Menu Background
You're almost done!
Now you just need to register your [MenuBackgroundType](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackgroundType.java) to the [MenuBackgroundTypeRegistry](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackgroundTypeRegistry.java) on game load and your new background is ready to use!

```java
package de.keksuccino.fancymenu;

import net.minecraftforge.fml.common.Mod;
import de.keksuccino.fancymenu.api.background.MenuBackgroundTypeRegistry;

@Mod("modid")
public class ExampleModMainClass {

    public ExampleModMainClass() {
        try {

            //Register your MenuBackgroundType to the MenuBackgroundTypeRegistry at mod init.
            MenuBackgroundTypeRegistry.registerBackgroundType(new ExampleMenuBackgroundType());

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

## 2.3. Creating an INPUT-STRING Background

[MenuBackgroundType](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackgroundType.java)s in the **input string mode** create [MenuBackground](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackground.java) instances on-the-fly, out of an input string.
These instances don't get stored like in **normal mode**. Everytime a layout gets loaded, new instances will be created.

### 2.3.1. The `MenuBackground` Class

Create a new subclass of the [MenuBackground](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackground.java) class and give it a fitting name.
In this case, I will name my example class `ExampleMenuBackgroundForInputString`.

There are some important things to take care of here.

#### 2.3.1.1. The Constructor
Other than in **normal mode**, it's not important to choose a **unique** identifier for your background here, since they don't get stored. It basically doesn't matter what identifiers you use for [MenuBackground](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackground.java) instances when in **input string mode**.

Of course it's still possible to set variables on construction here.

```java
public ExampleMenuBackgroundForInputString(@Nonnull MenuBackgroundType type, String imagePath) {
    //Identifiers aren't really used for backgrounds that don't get registered to a type (because the type uses the input string),
    //so just set something random here.
    super("unused_identifier", type);

    //Check if the image exists and has the correct file type, then load it.
    File imageFile = new File(imagePath);
    if (imageFile.exists() && (imageFile.getPath().toLowerCase().endsWith(".jpg") || imageFile.getPath().toLowerCase().endsWith(".jpeg") || imageFile.getPath().toLowerCase().endsWith(".png"))) {
        this.imageLocation = TextureHandler.getResource(imageFile.getPath());
        if (this.imageLocation != null) {
            this.imageLocation.loadTexture();
        }
    }

}
```

#### 2.3.1.2. The `onOpenMenu()` Method
This method is **unused** for backgrounds in **input string mode**, since new instances get created everytime a menu gets loaded anyways, so there's nothing to reset.

```java
@Override
public void onOpenMenu() {
    //Empty because everytime the menu gets opened, a new instance of the background will be created
    //when using input strings, so you don't need to reset stuff.
}
```

#### 2.3.1.3. The `render()` Method
This method gets called to render your menu background instance.
Should be self-explaining what to do here, right?

```java
//Here you will render the background instance.
//You should always render backgrounds over the full size of the screen, otherwise it will look ugly.
@Override
public void render(PoseStack matrix, Screen screen, boolean keepAspectRatio) {

    try {

        //Check if the image location is ready to get rendered
        if ((this.imageLocation != null) && this.imageLocation.isReady()) {

            RenderSystem.enableBlend();
            RenderUtils.bindTexture(this.imageLocation.getResourceLocation());
            RenderSystem.setShaderColor(1.0F, 1.0F, 1.0F, 1.0F);

            //If the keep-aspect-ratio toggle is disabled, just stretch the image background to the full size of the screen it is rendered in
            if (!keepAspectRatio) {

                GuiComponent.blit(matrix, 0, 0, 1.0F, 1.0F, screen.width, screen.height, screen.width, screen.height);

            //If the background image should keep its aspect ratio, try to keep the aspect ratio as long as possible.
            //As soon as it's not possible to keep the aspect ratio anymore, just stretch it.
            } else {

                int w = this.imageLocation.getWidth();
                int h = this.imageLocation.getHeight();
                double ratio = (double) w / (double) h;
                int wfinal = (int)(screen.height * ratio);
                int screenCenterX = screen.width / 2;
                if (wfinal < screen.width) {
                    GuiComponent.blit(matrix, 0, 0, 1.0F, 1.0F, screen.width, screen.height, screen.width, screen.height);
                } else {
                    GuiComponent.blit(matrix, screenCenterX - (wfinal / 2), 0, 1.0F, 1.0F, wfinal, screen.height, wfinal, screen.height);
                }

            }

        }

    } catch (Exception e) {
        e.printStackTrace();
    }

}
```

#### 2.3.1.4. Full Example Class

This is a full working [MenuBackground](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackground.java) example.

```java
package de.keksuccino.fancymenu.api.background.example.with_input_string;

import com.mojang.blaze3d.systems.RenderSystem;
import com.mojang.blaze3d.vertex.PoseStack;
import de.keksuccino.fancymenu.api.background.MenuBackground;
import de.keksuccino.fancymenu.api.background.MenuBackgroundType;
import de.keksuccino.konkrete.rendering.RenderUtils;
import de.keksuccino.konkrete.resources.ExternalTextureResourceLocation;
import de.keksuccino.konkrete.resources.TextureHandler;
import net.minecraft.client.gui.GuiComponent;
import net.minecraft.client.gui.screens.Screen;

import javax.annotation.Nonnull;
import java.io.File;

//This is an example menu background that renders an external image.
//It gets created by a background type that uses an input string to get the image file.
public class ExampleMenuBackgroundForInputString extends MenuBackground {

    private ExternalTextureResourceLocation imageLocation = null;

    public ExampleMenuBackgroundForInputString(@Nonnull MenuBackgroundType type, String imagePath) {
        //Identifiers aren't really used for backgrounds that don't get registered to a type (because the type uses the input string),
        //so just set something random here.
        super("unused_identifier", type);

        //Check if the image exists and has the correct file type, then load it.
        File imageFile = new File(imagePath);
        if (imageFile.exists() && (imageFile.getPath().toLowerCase().endsWith(".jpg") || imageFile.getPath().toLowerCase().endsWith(".jpeg") || imageFile.getPath().toLowerCase().endsWith(".png"))) {
            this.imageLocation = TextureHandler.getResource(imageFile.getPath());
            if (this.imageLocation != null) {
                this.imageLocation.loadTexture();
            }
        }

    }

    @Override
    public void onOpenMenu() {
        //Empty because everytime the menu gets opened, a new instance of the background will be created
        //when using input strings, so you don't need to reset stuff.
    }

    //Here you will render the background instance.
    //You should always render backgrounds over the full size of the screen, otherwise it will look ugly.
    @Override
    public void render(PoseStack matrix, Screen screen, boolean keepAspectRatio) {

        try {

            //Check if the image location is ready to get rendered
            if ((this.imageLocation != null) && this.imageLocation.isReady()) {

                RenderSystem.enableBlend();
                RenderUtils.bindTexture(this.imageLocation.getResourceLocation());
                RenderSystem.setShaderColor(1.0F, 1.0F, 1.0F, 1.0F);

                //If the keep-aspect-ratio toggle is disabled, just stretch the image background to the full size of the screen it is rendered in
                if (!keepAspectRatio) {

                    GuiComponent.blit(matrix, 0, 0, 1.0F, 1.0F, screen.width, screen.height, screen.width, screen.height);

                //If the background image should keep its aspect ratio, try to keep the aspect ratio as long as possible.
                //As soon as it's not possible to keep the aspect ratio anymore, just stretch it.
                } else {

                    int w = this.imageLocation.getWidth();
                    int h = this.imageLocation.getHeight();
                    double ratio = (double) w / (double) h;
                    int wfinal = (int)(screen.height * ratio);
                    int screenCenterX = screen.width / 2;
                    if (wfinal < screen.width) {
                        GuiComponent.blit(matrix, 0, 0, 1.0F, 1.0F, screen.width, screen.height, screen.width, screen.height);
                    } else {
                        GuiComponent.blit(matrix, screenCenterX - (wfinal / 2), 0, 1.0F, 1.0F, wfinal, screen.height, wfinal, screen.height);
                    }

                }

            }

        } catch (Exception e) {
            e.printStackTrace();
        }

    }
}
```

### 2.3.2. The `MenuBackgroundType` Class

Create a new subclass of the [MenuBackgroundType](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackgroundType.java) class and give it a fitting name.
In this case, I will name my example background type class `ExampleMenuBackgroundTypeWithInputString`.

There are some important things in this class you need to take care of.

#### 2.3.1.1. The Constructor
The constructor is used to set the **unique** identifier of your background type.

```java
public ExampleMenuBackgroundTypeWithInputString() {
    //This identifier needs to be UNIQUE! It is not possible to register multiple types with the same identifier.
    super("example_type_input_string");
}
```

#### 2.3.2.2. The `loadBackgrounds()` Method
This method is **unused** when in **input string mode**, since [MenuBackground](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackground.java) instances get created on-the-fly in this mode.

```java
@Override
    public void loadBackgrounds() {
    //Empty because background instances get created on-the-fly via createInstanceFromInputString()
}
```

#### 2.3.2.3. The `getDisplayName()` Method
Called to get the display name of the background type.
The display name is shown in the background options of the layout editor.

```java
//You don't really have much space for the display name, so try to choose a short one ond explain the type further in the description.
@Override
public String getDisplayName() {
    return "Example Type w/ Input";
}
```

#### 2.3.2.4. The `getDescription()` Method
Gets the description of the background type.
Shown in the background options of the layout editor.

```java
//Gets displayed when hovering over the type switcher in the background options menu in the layout editor.
//This is great for telling users everything important about your background type!
@Override
public List<String> getDescription() {
    List<String> l = new ArrayList<>();
    l.add("This is an example type");
    l.add("that uses input strings.");
    l.add("You can choose an image that");
    l.add("then gets displayed as background.");
    return l;
}
```

#### 2.3.2.5. The `needsInputString()` Method
This is one of the most important methods, because here you choose the mode of the background type.
In this case, we return `true` here, because we want the **input string mode** for our background type.

Returning `false` here would set the background type to the **normal mode**.

```java
@Override
public boolean needsInputString() {
    //Return true to set this background type to the "input string mode".
    //This means it will call the createInstanceFromInputString() method to create instances of your background,
    //instead of getting it from the loaded background instances.
    return true;
}
```

#### 2.3.2.6. The `createInstanceFromInputString()` Method
When in **input string mode**, this method gets called everytime a new [MenuBackground](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackground.java) instance is needed.
It's basically the menu background factory.

This method has the given **input string** as parameter, so you can use it to create the new instance from it.

```java
//In input string mode, this will get called whenever a new background instance is needed.
//Is called when opening a menu or when clicking on the input string button in the background options menu of the layout editor.
@Override
public MenuBackground createInstanceFromInputString(String inputString) {
    //Return a new background instance from the inputString.
    //In this case, the inputString is a path to an image file.
    return new ExampleMenuBackgroundForInputString(this, inputString);
}
```

#### 2.3.2.7. The `onInputStringButtonPress()` Method
Here is where you specify what happens when the user clicks on the input string button in the background options of the layout editor.
There are basically no limitations here, you can do whatever you want, as long as you properly set the new background to the editor instance at the end.

```java
//This gets called when the input string button in the background options is pressed by the user.
//You can basically do everything here.
@Override
public void onInputStringButtonPress(LayoutEditorScreen handler, BackgroundOptionsPopup optionsPopup) {

    //This is a file chooser popup to choose the image for the background.
    ChooseFilePopup cf = new ChooseFilePopup((filePath) -> {
        if (filePath != null) {
            //Always create a snapshot before changing the custom background fields!
            handler.history.saveSnapshot(handler.history.createSnapshot());
            //Always reset all backgrounds before setting a new one!
            optionsPopup.resetBackgrounds();
            //Always set the raw input string (file path in this case) to the input string field!
            handler.customMenuBackgroundInputString = filePath;
            //Create a new instance of your background and set it to the custom background field!
            handler.customMenuBackground = this.createInstanceFromInputString(filePath);
        }
        //This will open the parent popup again after choosing an image.
        PopupHandler.displayPopup(optionsPopup);
    }, "jpg", "jpeg", "png");
    if ((handler.customMenuBackgroundInputString != null)) {
        cf.setText(handler.customMenuBackgroundInputString);
    }
    //Open the file chooser popup.
    PopupHandler.displayPopup(cf);

}
```

#### The `inputStringButtonLabel()` Method
Returns the label button label of the input string button in the background options of the layout editor.

```java
//The button label of the input string button in the background options.
@Override
public String inputStringButtonLabel() {
    return "Choose File";
}
```

#### The `inputStringButtonTooltip()` Method
Returns the tooltip of the input string button in the background options of the layout editor.

```java
//A tooltip that gets displayed when hovering over the input string button in the background options menu of the layout editor.
@Override
public List<String> inputStringButtonTooltip() {
    List<String> l = new ArrayList<>();
    l.add("This is a button tooltip");
    l.add("for the 'Choose File' button.");
    return l;
}
```

#### 2.3.2.7 Full Example Class
This is a full working [MenuBackgroundType](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackgroundType.java) example.

```java
package de.keksuccino.fancymenu.api.background.example.with_input_string;

import de.keksuccino.fancymenu.api.background.MenuBackground;
import de.keksuccino.fancymenu.api.background.MenuBackgroundType;
import de.keksuccino.fancymenu.menu.fancy.helper.layoutcreator.LayoutEditorScreen;
import de.keksuccino.fancymenu.menu.fancy.helper.layoutcreator.content.BackgroundOptionsPopup;
import de.keksuccino.fancymenu.menu.fancy.helper.layoutcreator.content.ChooseFilePopup;
import de.keksuccino.konkrete.gui.screens.popup.PopupHandler;

import java.util.ArrayList;
import java.util.List;

//This is a background type that creates backgrounds out of user string inputs.
//It displays a "Choose File" button in the background options of the layout editor, so the user can choose a file for a background.
//This file path (input string) is then used to create an instance of the background.
public class ExampleMenuBackgroundTypeWithInputString extends MenuBackgroundType {

    public ExampleMenuBackgroundTypeWithInputString() {
        //This identifier needs to be UNIQUE! It is not possible to register multiple types with the same identifier.
        super("example_type_input_string");
    }

    @Override
    public void loadBackgrounds() {
        //Empty because background instances get created on-the-fly via createInstanceFromInputString()
    }

    //You don't really have much space for the display name, so try to choose a short one ond explain the type further in the description.
    @Override
    public String getDisplayName() {
        return "Example Type w/ Input";
    }

    //Gets displayed when hovering over the type switcher in the background options menu in the layout editor.
    //This is great for telling users everything important about your background type!
    @Override
    public List<String> getDescription() {
        List<String> l = new ArrayList<>();
        l.add("This is an example type");
        l.add("that uses input strings.");
        l.add("You can choose an image that");
        l.add("then gets displayed as background.");
        return l;
    }

    @Override
    public boolean needsInputString() {
        //Return true to set this background type to the "input string mode".
        //This means it will call the createInstanceFromInputString() method to create instances of your background,
        //instead of getting it from the loaded background instances.
        return true;
    }

    //In input string mode, this will get called whenever a new background instance is needed.
    //Is called when opening a menu or when clicking on the input string button in the background options menu of the layout editor.
    @Override
    public MenuBackground createInstanceFromInputString(String inputString) {
        //Return a new background instance from the inputString.
        return new ExampleMenuBackgroundForInputString(this, inputString);
    }

    //This gets called when the input string button in the background options is pressed by the user.
    //You can basically do everything here.
    @Override
    public void onInputStringButtonPress(LayoutEditorScreen handler, BackgroundOptionsPopup optionsPopup) {

        //This is a file chooser popup to choose the image for the background.
        ChooseFilePopup cf = new ChooseFilePopup((filePath) -> {
            if (filePath != null) {
                //Always create a snapshot before changing the custom background fields!
                handler.history.saveSnapshot(handler.history.createSnapshot());
                //Always reset all backgrounds before setting a new one!
                optionsPopup.resetBackgrounds();
                //Always set the raw input string (file path in this case) to the input string field!
                handler.customMenuBackgroundInputString = filePath;
                //Create a new instance of your background and set it to the custom background field!
                handler.customMenuBackground = this.createInstanceFromInputString(filePath);
            }
            //This will open the parent popup again after choosing an image.
            PopupHandler.displayPopup(optionsPopup);
        }, "jpg", "jpeg", "png");
        if ((handler.customMenuBackgroundInputString != null)) {
            cf.setText(handler.customMenuBackgroundInputString);
        }
        //Open the file chooser popup.
        PopupHandler.displayPopup(cf);

    }

    //The button label of the input string button in the background options.
    @Override
    public String inputStringButtonLabel() {
        return "Choose File";
    }

    //A tooltip that gets displayed when hovering over the input string button in the background options menu of the layout editor.
    @Override
    public List<String> inputStringButtonTooltip() {
        List<String> l = new ArrayList<>();
        l.add("This is a button tooltip");
        l.add("for the 'Choose File' button.");
        return l;
    }

}
```

### 2.3.3. Registering the Menu Background
You're almost done!
Now you just need to register your [MenuBackgroundType](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackgroundType.java) to the [MenuBackgroundTypeRegistry](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/background/MenuBackgroundTypeRegistry.java) on game load and your new background is ready to use!

```java
package de.keksuccino.fancymenu;

import net.minecraftforge.fml.common.Mod;
import de.keksuccino.fancymenu.api.background.MenuBackgroundTypeRegistry;

@Mod("modid")
public class ExampleModMainClass {

    public ExampleModMainClass() {
        try {

            //Register your MenuBackgroundType to the MenuBackgroundTypeRegistry at mod init.
            MenuBackgroundTypeRegistry.registerBackgroundType(new ExampleMenuBackgroundTypeWithInputString());

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```