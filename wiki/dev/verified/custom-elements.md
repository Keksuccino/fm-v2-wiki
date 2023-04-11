---
title: [DEV] Custom Elements
description: Create custom layout elements using the FancyMenu API.
published: true
date: 2023-04-11T01:19:55.871Z
tags: api
editor: markdown
dateCreated: 2023-04-07T04:32:23.095Z
---

# 0. About
The FancyMenu API allows you to add your own custom elements via an extension mod, so you can use them in layouts.

# 1. Preparing Your Workspace
To prepare your workspace for the FancyMenu API, please take a look at the [Preparing The Workspace](./prepare-workspace) wiki page.

# 2. Adding New Elements
Every custom element (or **item**, as elements are called internally) needs to be wrapped into a [CustomizationItemContainer](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/CustomizationItemContainer.java).
This container needs to be registered to the [CustomizationItemRegistry](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/CustomizationItemRegistry.java) on mod init.

## 2.1. Creating the Item
The actual class of items is [CustomizationItem](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/CustomizationItem.java). This class is the item body which renders it and stores all of its properties.

Create a new subclass of [CustomizationItem](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/CustomizationItem.java) for your item and give it a fitting name.
In this case, I will name my example item class `ExampleCustomizationItem`.

There are two important things in this class.

### 2.1.1. The Constructor
The first important thing is the class constructor.
Here you need to de-serialize properties of saved/serialized item instances and set it to the new real instance.
Items get serialized to `PropertiesSection`s, when saved to a layout.

You just need to care about your own custom item values here. Basic stuff like item width, height, orientation, X position and Y poosition are part of every item by default and get handled by the superclass.

```java
//The constuctor is used to de-serialize the PropertiesSection and set all of its values to the new real item instance.
public ExampleCustomizationItem(CustomizationItemContainer parentContainer, PropertiesSection item) {

    //The superclass will automatically get values like orientation, x pos, y pos, width and height and will set it to the real item instance.
    super(parentContainer, item);

    //Getting a custom property from the serialized item instance and set it to the real instance
    String someProperty = item.getEntryValue("saved_property");
    if (someProperty != null) {
        this.someField = someProperty;
    }

}
```

### 2.1.2. The `render()` Method
The second important thing. Here you will render your item (duh).
This is basically your item body. The visible part of your item. What you see in the menu later.

So just do your thing here, you know?

The only **really necessary** part here is to wrap everything in this method into `shouldRender()`.
This method checks for visibility requirements and other important stuff. So don't forget this, okay?

```java
@Override
public void render(PoseStack matrix, Screen menu) throws IOException {

    //This is really important and should be in every item render method, to check for visibility requirements and more.
    if (this.shouldRender()) {

        //Always use getPosX() and getPosY() to get the X and Y positions of the item.
        //The fields posX and posY aren't the final position, just the base pos without the orientation!
        int x = this.getPosX(menu);
        int y = this.getPosY(menu);
      
        //We want to use placeholder text values for our 'someField' string, so we use the DynamicValueHelper to convert them,
        //but they should look like placeholders in the editor, so we only convert them when not in the editor.
        String text;
        if (!isEditorActive()) {
            text = DynamicValueHelper.convertFromRaw(this.someField);
        } else {
            text = StringUtils.convertFormatCodes(this.someField, "&", "Â§");
        }

        //Always try to make your items' opacity changeable by setting the 'opacity' field!
        //This field is set by the "delay appearance" feature to control the fade-in opacity.
        drawString(matrix, Minecraft.getInstance().font, text, x + 10, y + 10, -1 | Mth.ceil(this.opacity * 255.0F) << 24);

    }

}
```

### 2.1.3. Full Example
Here is a full working [CustomizationItem](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/CustomizationItem.java) example.

```java
package de.keksuccino.fancymenu.api.item.example;

import com.mojang.blaze3d.systems.RenderSystem;
import com.mojang.blaze3d.vertex.PoseStack;
import de.keksuccino.fancymenu.api.item.CustomizationItem;
import de.keksuccino.fancymenu.api.item.CustomizationItemContainer;
import de.keksuccino.fancymenu.menu.fancy.DynamicValueHelper;
import de.keksuccino.konkrete.input.StringUtils;
import de.keksuccino.konkrete.properties.PropertiesSection;
import de.keksuccino.konkrete.rendering.RenderUtils;
import net.minecraft.client.Minecraft;
import net.minecraft.client.gui.screens.Screen;
import net.minecraft.util.Mth;

import java.awt.*;
import java.io.IOException;

public class ExampleCustomizationItem extends CustomizationItem {

    public String displayText = "placeholder";
    public String backgroundColorString = "#38ff38";
    public Color backgroundColor = new Color(56, 255, 56);

    //The constuctor is used to de-serialize the PropertiesSection and set all of its values to the new real item instance.
    public ExampleCustomizationItem(CustomizationItemContainer parentContainer, PropertiesSection item) {

        //The superclass will automatically get values like orientation, x pos, y pos, width and height and will set it to the real item instance.
        super(parentContainer, item);

        //Getting the background HEX color from the serialized item
        String backColorHex = item.getEntryValue("background_color");
        if (backColorHex != null) {
            Color c = RenderUtils.getColorFromHexString(backColorHex);
            if (c != null) {
                this.backgroundColor = c;
                this.backgroundColorString = backColorHex;
            }
        }

        //Getting the display text string from the serialized item
        String dText = item.getEntryValue("display_text");
        if (dText != null) {
            this.displayText = dText;
        }

    }

    @Override
    public void render(PoseStack matrix, Screen menu) throws IOException {

        //This is really important and should be in every item render method, to check for visibility requirements and more.
        if (this.shouldRender()) {

            //Always use getPosX() and getPosY() to get the X and Y positions of the item.
            //The fields posX and posY aren't the final position, just the base pos without the orientation!
            int x = this.getPosX(menu);
            int y = this.getPosY(menu);

            RenderSystem.enableBlend();

            //Rendering the background color as background of the item.
            fill(matrix, x, y, x + this.getWidth(), y + this.getHeight(), this.backgroundColor.getRGB() | Mth.ceil(this.opacity * 255.0F) << 24);

            //Rendering the display text to the upper-left side of the item
            if (this.displayText != null) {
                //We want to use placeholder text values for the display text, so we use the DynamicValueHelper to convert them,
                //but they should look like placeholders in the editor, so we only convert them when not in the editor.
                String text;
                if (!isEditorActive()) {
                    text = DynamicValueHelper.convertFromRaw(this.displayText);
                } else {
                    text = StringUtils.convertFormatCodes(this.displayText, "&", "Â§");
                }
                //The 'opacity' field is used to set the fade-in opacity of the item when the "delay appearance" option is enabled for it.
                //Always try to make your items' opacity changeable by setting the 'opacity' field! (I also used it in the fill method for the background)
                drawString(matrix, Minecraft.getInstance().font, text, x + 10, y + 10, -1 | Mth.ceil(this.opacity * 255.0F) << 24);
            }

        }

    }

}
```

## 2.2. Creating the Editor Element
[LayoutEditorElement](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/LayoutEditorElement.java)s contain everything that's important for your item when in the [layout editor](./24x-Layout-Editor).
This includes all UI parts related to your item, like the **context menu when right-clicking an item** in the editor.

Create a new subclass of [LayoutEditorElement](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/LayoutEditorElement.java) for your item and give it a fitting name.
In this case, I will name my example editor element class `ExampleLayoutEditorElement`.

There are two important methods in this class that need your attention.

### 2.2.1. The `init()` Method
This is the first important method and is called by the editor to initialize your editor element (mostly to initalize the UI).

Every editor element has a `rightclickMenu` field. This is the right-click context menu if the element.
This context menu already contains all the default stuff like setting the orientation, deleting the element, etc.

If you now want to make it possible to edit your own custom values of your item here, you need to add new entries to said context menu and link them to your item.

The `object` field of the editor element class is your actual [CustomizationItem](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/CustomizationItem.java) instance, just cast it to your item subclass (`ExampleCustomizationItem` in this case) to use its custom fields and methods.

```java
@Override
public void init() {

    //The superclass adds basic stuff to the right-click context menu, like visibility requirement controls, delete controls, orientation, etc.
    super.init();

    //The 'object' field holds the CustomizationItem instance of this element.
    //Cast it to your own item class, to get and set your own fields.
    ExampleCustomizationItem i = ((ExampleCustomizationItem)this.object);

    //This button will be part of the right-click context menu of the element and is used to change the 'someField' field of the CustomizationItem subclass.
    AdvancedButton someFieldButton = new AdvancedButton(0, 0, 0, 0, "Set Some Field", (press) -> {
        //This is the basic input popup for text content, used in many parts of FancyMenu.
        FMTextInputPopup pop = new FMTextInputPopup(new Color(0, 0, 0, 0), "Set Some Field Content", null, 240, (callback) -> {
            //The callback of popups will be null, when pressing ESC in it to force-close it.
            if (callback != null) {
                if (!callback.equals(i.someField)) {
                    //Create a snapshot before every change, so you can undo the change in the editor (using CTRL + Z)
                    this.handler.history.saveSnapshot(this.handler.history.createSnapshot());
                    //Now set the new value to the item instance
                    i.someField = callback;
                }
            }
        });
        //Set the current value as default text of the text input popup
        if (i.someField != null) {
            pop.setText(i.someField);
        }
        //Open the popup
        PopupHandler.displayPopup(pop);
    });
    someFieldButton.setDescription("This is just an example button tooltip.");
    //Add the button to the right-click context menu content
    this.rightclickMenu.addContent(someFieldButton);

}
```

### 2.2.2. The `serializeItem()` Method
Simple but important! The second important method is called when saving the layout.
Here your item instance (`object` field) gets serialized to a `SimplePropertiesSection` to save its properties in the layout file.

All the default stuff like width, height, orientation, X pos, Y pos, visibility requirements and more will be automatically added to the serialized instance, so you just need to care about your own custom values here.

```java
@Override
public SimplePropertiesSection serializeItem() {

    ExampleCustomizationItem i = ((ExampleCustomizationItem)this.object);

    SimplePropertiesSection sec = new SimplePropertiesSection();

    //Add your custom item values here, so they get saved and can later be de-serialized again.
    sec.addEntry("saved_property", i.someField);

    return sec;

}
```

### 2.2.3. Full Example
Here is a full working [LayoutEditorElement](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/LayoutEditorElement.java) example.

```java
package de.keksuccino.fancymenu.api.item.example;

import de.keksuccino.fancymenu.api.item.LayoutEditorElement;
import de.keksuccino.fancymenu.menu.fancy.helper.DynamicValueInputPopup;
import de.keksuccino.fancymenu.menu.fancy.helper.layoutcreator.LayoutEditorScreen;
import de.keksuccino.fancymenu.menu.fancy.helper.ui.popup.FMTextInputPopup;
import de.keksuccino.konkrete.gui.content.AdvancedButton;
import de.keksuccino.konkrete.gui.screens.popup.PopupHandler;
import de.keksuccino.konkrete.rendering.RenderUtils;

import java.awt.*;

public class ExampleLayoutEditorElement extends LayoutEditorElement {

    public ExampleLayoutEditorElement(ExampleCustomizationItemContainer parentContainer, ExampleCustomizationItem customizationItemInstance, LayoutEditorScreen handler) {
        super(parentContainer, customizationItemInstance, true, handler, true);
    }

    @Override
    public void init() {

        //The superclass adds basic stuff to the right-click context menu, like visibility requirement controls, delete controls, orientation, etc.
        super.init();

        //The 'object' field holds the CustomizationItem instance of this element.
        //Cast it to your own item class, to get and set your own fields.
        ExampleCustomizationItem i = ((ExampleCustomizationItem)this.object);

        //This button will be part of the right-click context menu of the element and is uses to change the background color value of the item.
        AdvancedButton backgroundColorButton = new AdvancedButton(0, 0, 0, 0, "Background Color", (press) -> {
            //This is the basic input popup for text content, used in many parts of FancyMenu.
            FMTextInputPopup pop = new FMTextInputPopup(new Color(0, 0, 0, 0), "Background Color HEX", null, 240, (callback) -> {
                //The callback of popups will be null, when pressing ESC in it to force-close it.
                if (callback != null) {
                    if (!callback.equals(i.backgroundColorString)) {
                        Color c = RenderUtils.getColorFromHexString(callback);
                        if (c != null) {
                            //Create a snapshot before every change, so you can undo the change in the editor (using CTRL + Z)
                            this.handler.history.saveSnapshot(this.handler.history.createSnapshot());
                            //Now set the new values to the item instance
                            i.backgroundColorString = callback;
                            i.backgroundColor = c;
                        }
                    }
                }
            });
            //Set the current value as default text of the text input popup
            if (i.backgroundColorString != null) {
                pop.setText(i.backgroundColorString);
            }
            //Open the popup
            PopupHandler.displayPopup(pop);
        });
        backgroundColorButton.setDescription("This is just an example button tooltip.");
        //Add the button to the right-click context menu content
        this.rightclickMenu.addContent(backgroundColorButton);

        //This is the button to change the display text of the item. Will also be part of the right-click context menu.
        AdvancedButton displayTextButton = new AdvancedButton(0, 0, 0, 0, "Display Text", (press) -> {
            //This is also a text input popup, but with placeholder text value support (the little icon at the right side of the input field)
            DynamicValueInputPopup pop = new DynamicValueInputPopup(new Color(0, 0, 0, 0), "Set Display Text", null, 240, (callback) -> {
                if (callback != null) {
                    if (!callback.equals(i.displayText)) {
                        //Again, save a snapshot before changing something!
                        this.handler.history.saveSnapshot(this.handler.history.createSnapshot());
                        //Setting the new display text value
                        i.displayText = callback;
                    }
                }
            });
            if (i.displayText != null) {
                pop.setText(i.displayText);
            }
            PopupHandler.displayPopup(pop);
        });
        this.rightclickMenu.addContent(displayTextButton);

    }

    @Override
    public SimplePropertiesSection serializeItem() {

        ExampleCustomizationItem i = ((ExampleCustomizationItem)this.object);

        SimplePropertiesSection sec = new SimplePropertiesSection();

        //Add your custom item values here, so they get saved and can later be de-serialized again.
        sec.addEntry("background_color", i.backgroundColorString);
        sec.addEntry("display_text", i.displayText);

        return sec;

    }

}
```

## 2.3. Creating the Container
The last class we need for our item is a subclass of [CustomizationItemContainer](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/CustomizationItemContainer.java).
This container is basically an instance builder for [CustomizationItem](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/CustomizationItem.java)s and [LayoutEditorElement](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/LayoutEditorElement.java)s.

Create a new subclass of [CustomizationItemContainer](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/CustomizationItemContainer.java) for your item and give it a fitting name.
In this case, I will name my example container class `ExampleCustomizationItemContainer`.

### 2.3.1. The Item Identifier
The constructor of the item container needs a **unique item identifier**.
This identifier needs to be unique, it's not possible to register two items with the same identifier, so just use something like your username as prefix.

You should just set this identifier directly in the subclass constructor.

```java
public ExampleCustomizationItemContainer() {
    super("example_item_identifier");
}
```

### 2.3.2. The Instance Builders
The item container is used to build instances of your [CustomizationItem](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/CustomizationItem.java) subclass and your [LayoutEditorElement](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/LayoutEditorElement.java) subclass.
You need to set up the builder methods so the container can construct instances of your subclasses.

```java
//This will construct a default instance of your CustomizationItem without any customizations made to it.
@Override
public CustomizationItem constructDefaultItemInstance() {
    //Just use an empty properties section here.
    //Make sure that your CustomizationItem accepts empty sections without throwing errors!
    ExampleCustomizationItem i = new ExampleCustomizationItem(this, new PropertiesSection("dummy"));
    //The default size of 10x10 would be a bit too small for the item, so I set a new default size of 100x100 to the default instance.
    //This means that now every new item of this type will have a size of 100x100 by default.
    i.width = 100;
    i.height = 100;
    return i;
}

//This will construct a customized instance of your CustomizationItem, using the given PropertiesSection (serialized item) to set all customizations.
@Override
public CustomizationItem constructCustomizedItemInstance(PropertiesSection serializedItem) {
    return new ExampleCustomizationItem(this, serializedItem);
}

//This will construct a new instance of your LayoutEditorElement, used in the layout editor.
@Override
public LayoutEditorElement constructEditorElementInstance(CustomizationItem item, LayoutEditorScreen handler) {
    return new ExampleLayoutEditorElement(this, (ExampleCustomizationItem) item, handler);
}
```

### 2.3.4. The Display Name
You need to set a display name for your item.
This display name is used in the [layout editor](./24x-Layout-Editor).

The method allows you to localize the display name.

```java
@Override
public String getDisplayName() {
    return "Example Item";
}
```

### 2.3.5. The Description
The description of your item is displayed when hovering over the button to add a new item of this type in the [layout editor](./24x-Layout-Editor).

```java
@Override
public String[] getDescription() {
    return new String[] {
        "This is a description",
        "with 2 lines of text."
    };
}
```

### 2.3.6. Full Example
Here is a full working [CustomizationItemContainer](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/CustomizationItemContainer.java) example.

```java
package de.keksuccino.fancymenu.api.item.example;

import de.keksuccino.fancymenu.api.item.CustomizationItem;
import de.keksuccino.fancymenu.api.item.CustomizationItemContainer;
import de.keksuccino.fancymenu.api.item.LayoutEditorElement;
import de.keksuccino.fancymenu.menu.fancy.helper.layoutcreator.LayoutEditorScreen;
import de.keksuccino.konkrete.properties.PropertiesSection;

//This needs to be registered to the CustomizationItemRegistry at mod init
public class ExampleCustomizationItemContainer extends CustomizationItemContainer {

    public ExampleCustomizationItemContainer() {
        super("example_item_identifier");
    }

    @Override
    public CustomizationItem constructDefaultItemInstance() {
        ExampleCustomizationItem i = new ExampleCustomizationItem(this, new PropertiesSection("dummy"));
        //The default size of 10x10 would be a bit too small for the item, so I set a new default size of 100x100 to the default instance.
        //This means that now every new item of this type will have a size of 100x100 by default.
        i.width = 100;
        i.height = 100;
        return i;
    }

    @Override
    public CustomizationItem constructCustomizedItemInstance(PropertiesSection serializedItem) {
        return new ExampleCustomizationItem(this, serializedItem);
    }

    @Override
    public LayoutEditorElement constructEditorElementInstance(CustomizationItem item, LayoutEditorScreen handler) {
        return new ExampleLayoutEditorElement(this, (ExampleCustomizationItem) item, handler);
    }

    @Override
    public String getDisplayName() {
        return "Example Item";
    }

    @Override
    public String[] getDescription() {
        return new String[] {
                "This is a description",
                "with 2 lines of text."
        };
    }

}
```

## 2.4. Registering The Container
You're almost done! Just one last, important step.

FancyMenu needs to know about your custom item, so you need to register your [CustomizationItemContainer](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/CustomizationItemContainer.java) to the [CustomizationItemRegistery](https://github.com/Keksuccino/FancyMenu/blob/forge-1.17/src/main/java/de/keksuccino/fancymenu/api/item/CustomizationItemRegistry.java) when your extension mod gets initialized.

```java
package de.keksuccino.fancymenu;

import net.minecraftforge.fml.common.Mod;
import de.keksuccino.fancymenu.api.item.CustomizationItemRegistry;

@Mod("modid")
public class ExampleModMainClass {
	
	public ExampleModMainClass() {
		try {
			
            //Register your CustomizationItemContainer to the CustomizationItemRegistry at mod init.
            CustomizationItemRegistry.registerItem(new ExampleCustomizationItemContainer());
	    	
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

}
```

Now you can use your own item in layouts!