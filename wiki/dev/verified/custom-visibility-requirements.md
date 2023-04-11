---
title: [DEV] Custom Visibility Requirements
description: Create custom visibility requirements using the FancyMenu API.
published: true
date: 2023-04-11T01:19:03.929Z
tags: api
editor: markdown
dateCreated: 2023-04-07T04:32:28.563Z
---

# 0. About
The FancyMenu API allows you to add your own custom visibility requirements via an extension mod, so you can use them for elements in layouts.

> **IMPORTANT**: The Visibility Requirement API is only available in FancyMenu v2.6.3+ !
{.is-warning}

# 1. Preparing Your Workspace
To prepare your workspace for the FancyMenu API, please take a look at the [Preparing The Workspace](./prepare-workspace) wiki page.

# 2. Adding Visibility Requirements
Visibility requirements use the [VisibilityRequirement](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/visibilityrequirements/VisibilityRequirement.java) class.
You need to create one subclass of [VisibilityRequirement](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/visibilityrequirements/VisibilityRequirement.java) per requirement.

Every [VisibilityRequirement](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/visibilityrequirements/VisibilityRequirement.java) needs to be registered to the [VisibilityRequirementRegistry](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/visibilityrequirements/VisibilityRequirementRegistry.java) at mod init.

## 2.1. Different Kinds of Requirements
Visibility requirements can be used in two different "modes".

The first one uses no value as input to check if the requirement is met, and the second one uses one.
If a requirement uses a value, the user needs to input this value when setting the requirement to an element.

## 2.2. Creating an Requirement WITHOUT Value
Create a new subclass of the [VisibilityRequirement](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/visibilityrequirements/VisibilityRequirement.java) class and give it a fitting name.
In this case, I will name my example class `ExampleVisibilityRequirement`.

There are some important things to take care of here.

### 2.2.1 The Constructor
The constructor is where you define the **unique** identifier of your requirement.

```java
public ExampleVisibilityRequirement() {
    //The identifier needs to be unique! It's not possible to register multiple requirements with the same identifier!
    super("example_requirement_no_value");
}
```

### 2.2.2 The `hasValue()` Method
This method returns if the requirement needs a value or not.
Since we don't want to use a value for this requirement, we just return `false`.

```java
@Override
public boolean hasValue() {
    //We don't need a value in this requirement, so we return false here.
    return false;
}
```

### 2.2.3. The `isRequirementMet()` Method
This is the most important method of your requirement.
It returns if the condition to check for in this requirement is met.

The method has the value of the requirement as parameter, but since this requirement has no value, the parameter will be `null`.

```java
//Here you return if the requirement is met (using the given requirement value if the requirement has one).
//We don't use a value in this example, so the parameter will be NULL and we can ignore it.
@Override
public boolean isRequirementMet(@Nullable String value) {

    //In this example, we just check if the window is in fullscreen mode and if it is, then we return true.
    return Minecraft.getInstance().options.fullscreen;

}
```

### 2.2.4. The `getDisplayName()` Method
This method returns the display name of the requirement.
The display name is shown in the visibility requirement options of the layout editor.

```java
//This is the display name of the requirement.
//You don't have much space for the display name, so try to choose a short one.
@Override
public String getDisplayName() {
    return "Example Requirement [No Value]";
}
```

### 2.2.5. The `getDescription()` Method
Returns the description of the requirement.
This description is displayed as tooltip when hovering over the toggle requirement button.

```java
//This is the description of the requirement.
@Override
public List<String> getDescription() {
    List<String> l = new ArrayList<>();
    l.add("This is an example requirement");
    l.add("without a value.");
    l.add("It checks if the window is in fullscreen.");
    return l;
}
```

### 2.2.6. The `getValueDisplayName()` Method
This method returns the display name of the value.
We don't use a value for this requirement, so we just return `null` here.

```java
//Since this requirement has no value, just return NULL here.
@Override
public String getValueDisplayName() {
    return null;
}
```

### 2.2.7. The `getValuePreset()` Method
Returns the content that is automatically set to the value input text field.
There is no value input field for this requirement, so we return `null`.

```java
//No value, so just return NULL.
@Override
public String getValuePreset() {
    return null;
}
```

### 2.2.8. The `getValueInputFieldFilter()` Method
The method returns a character filter that is being used to check for allowed chars the user can type into the value input text field.
No value for this requirement, that's why we return `null`.

```java
//You know the drill. No value = return NULL.
@Override
public CharacterFilter getValueInputFieldFilter() {
    return null;
}
```

### 2.2.9. Full Example Class
This is a full working [VisibilityRequirement](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/visibilityrequirements/VisibilityRequirement.java) example.

```java
package de.keksuccino.fancymenu.api.visibilityrequirements.example;

import de.keksuccino.fancymenu.api.visibilityrequirements.VisibilityRequirement;
import de.keksuccino.konkrete.input.CharacterFilter;
import net.minecraft.client.Minecraft;

import javax.annotation.Nullable;
import java.util.ArrayList;
import java.util.List;

public class ExampleVisibilityRequirement extends VisibilityRequirement {

    public ExampleVisibilityRequirement() {
        //The identifier needs to be unique! It's not possible to register multiple requirements with the same identifier!
        super("example_requirement_no_value");
    }

    @Override
    public boolean hasValue() {
        //We don't need a value in this requirement, so we return false here.
        return false;
    }

    //Here you return if the requirement is met (using the given requirement value if the requirement has one).
    //We don't use a value in this example, so the parameter will be NULL and we can ignore it.
    @Override
    public boolean isRequirementMet(@Nullable String value) {

        //In this example, we just check if the window is in fullscreen mode and if it is, then we return true.
        return Minecraft.getInstance().options.fullscreen;

    }

    //This is the display name of the requirement.
    //You don't have much space for the display name, so try to choose a short one.
    @Override
    public String getDisplayName() {
        return "Example Requirement [No Value]";
    }

    //This is the description of the requirement.
    @Override
    public List<String> getDescription() {
        List<String> l = new ArrayList<>();
        l.add("This is an example requirement");
        l.add("without a value.");
        l.add("It checks if the window is in fullscreen.");
        return l;
    }

    //Since this requirement has no value, just return NULL here.
    @Override
    public String getValueDisplayName() {
        return null;
    }

    //No value, so just return NULL.
    @Override
    public String getValuePreset() {
        return null;
    }

    //You know the drill. No value = return NULL.
    @Override
    public CharacterFilter getValueInputFieldFilter() {
        return null;
    }

}
```

### 2.2.10. Registering the Visibility Requirement
You're almost done!
Now you just need to register your [VisibilityRequirement](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/visibilityrequirements/VisibilityRequirement.java) to the [VisibilityRequirementRegistry](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/visibilityrequirements/VisibilityRequirementRegistry.java) on game load and your new visibility requirement is ready to use!

```java
package de.keksuccino.fancymenu;

import net.minecraftforge.fml.common.Mod;
import de.keksuccino.fancymenu.api.visibilityrequirements.VisibilityRequirementRegistry;

@Mod("modid")
public class ExampleModMainClass {

    public ExampleModMainClass() {
        try {

            //Register your VisibilityRequirement to the VisibilityRequirementRegistry at mod init.
            VisibilityRequirementRegistry.registerRequirement(new ExampleVisibilityRequirement());

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

## 2.3. Creating an Requirement WITH Value
Create a new subclass of the [VisibilityRequirement](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/visibilityrequirements/VisibilityRequirement.java) class and give it a fitting name.
In this case, I will name my example class `ExampleVisibilityRequirementWithValue`.

There are some important things to take care of here.

### 2.3.1 The Constructor
The constructor is where you define the **unique** identifier of your requirement.

```java
public ExampleVisibilityRequirementWithValue() {
    //The identifier needs to be unique! It's not possible to register multiple requirements with the same identifier!
    super("example_requirement_with_value");
}
```

### 2.3.2 The `hasValue()` Method
This method returns if the requirement needs a value or not.
We want to use a value for this requirement, so we return `true`.

```java
@Override
public boolean hasValue() {
    //This requirement needs a value, so we return true here.
    return true;
}
```

### 2.3.3. The `isRequirementMet()` Method
This is the most important method of your requirement.
It returns if the condition to check for in this requirement is met.

The method has the value of the requirement as parameter, so you can use it to check if the requirement is met.

```java
//Here you return if the requirement is met (using the given requirement value if the requirement has one).
//Since this requirement has a value, the value parameter will be the value of a requirement in a layout.
@Override
public boolean isRequirementMet(@Nullable String value) {

    //This requirement has a value that can be any string, but the requirement will only be met if the value is "show_me".
    //We return true if the value is "show_me".
    if (value != null) {
        return value.equalsIgnoreCase("show_me");
    }

    return false;

}
```

### 2.3.4. The `getDisplayName()` Method
This method returns the display name of the requirement.
The display name is shown in the visibility requirement options of the layout editor.

```java
//This is the display name of the requirement.
//You don't have much space for the display name, so try to choose a short one.
@Override
public String getDisplayName() {
    return "Example Requirement [With Value]";
}
```

### 2.3.5. The `getDescription()` Method
Returns the description of the requirement.
This description is displayed as tooltip when hovering over the toggle requirement button.

```java
//This is the description of the requirement.
@Override
public List<String> getDescription() {
    List<String> l = new ArrayList<>();
    l.add("This is an example requirement");
    l.add("with a value.");
    l.add("It checks if the value is 'show_me'.");
    return l;
}
```

### 2.3.6. The `getValueDisplayName()` Method
This method returns the display name of the value.

```java
//This is the display name of the VALUE of the requirement.
//You don't have much space for the display name, so try to choose a short one.
@Override
public String getValueDisplayName() {
    return "Example Value Name";
}
```

### 2.3.7. The `getValuePreset()` Method
Returns the content that is automatically set to the value input text field, if there is no real value already.
Good to show the user an example of a real value.

```java
//This is the content that will be automatically set to the value input field when there is no value already.
@Override
public String getValuePreset() {
    return "cool value preset";
}
```

### 2.3.8. The `getValueInputFieldFilter()` Method
The method returns a character filter that is being used to check for allowed chars the user can type into the value input text field.

If you want too allow all characters, just return `null` here.

```java
//The character filter of the value input field. Return NULL if you want to allow all characters.
//Can be used to only allow numbers in the input field, etc.
@Override
public CharacterFilter getValueInputFieldFilter() {
    return null;
}
```

### 2.3.9. Full Example Class
This is a full working [VisibilityRequirement](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/visibilityrequirements/VisibilityRequirement.java) example.

```java
package de.keksuccino.fancymenu.api.visibilityrequirements.example;

import de.keksuccino.fancymenu.api.visibilityrequirements.VisibilityRequirement;
import de.keksuccino.konkrete.input.CharacterFilter;

import javax.annotation.Nullable;
import java.util.ArrayList;
import java.util.List;

public class ExampleVisibilityRequirementWithValue extends VisibilityRequirement {

    public ExampleVisibilityRequirementWithValue() {
        //The identifier needs to be unique! It's not possible to register multiple requirements with the same identifier!
        super("example_requirement_with_value");
    }

    @Override
    public boolean hasValue() {
        //This requirement needs a value, so we return true here.
        return true;
    }

    //Here you return if the requirement is met (using the given requirement value if the requirement has one).
    //Since this requirement has a value, the value parameter will be the value of a requirement in a layout.
    @Override
    public boolean isRequirementMet(@Nullable String value) {

        //This requirement has a value that can be any string, but the requirement will only be met if the value is "show_me".
        //We return true if the value is "show_me".
        if (value != null) {
            return value.equalsIgnoreCase("show_me");
        }

        return false;

    }

    //This is the display name of the requirement.
    //You don't have much space for the display name, so try to choose a short one.
    @Override
    public String getDisplayName() {
        return "Example Requirement [With Value]";
    }

    //This is the description of the requirement.
    @Override
    public List<String> getDescription() {
        List<String> l = new ArrayList<>();
        l.add("This is an example requirement");
        l.add("with a value.");
        l.add("It checks if the value is 'show_me'.");
        return l;
    }

    //This is the display name of the VALUE of the requirement.
    //You don't have much space for the display name, so try to choose a short one.
    @Override
    public String getValueDisplayName() {
        return "Example Value Name";
    }

    //This is the content that will be automatically set to the value input field when there is no value already.
    @Override
    public String getValuePreset() {
        return "cool value preset";
    }

    //The character filter of the value input field. Return NULL if you want to allow all characters.
    //Can be used to only allow numbers in the input field, etc.
    @Override
    public CharacterFilter getValueInputFieldFilter() {
        return null;
    }

}
```

### 2.3.10. Registering the Visibility Requirement
You're almost done!
Now you just need to register your [VisibilityRequirement](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/visibilityrequirements/VisibilityRequirement.java) to the [VisibilityRequirementRegistry](https://github.com/Keksuccino/FancyMenu/blob/forge-1.18/src/main/java/de/keksuccino/fancymenu/api/visibilityrequirements/VisibilityRequirementRegistry.java) on game load and your new visibility requirement is ready to use!

```java
package de.keksuccino.fancymenu;

import net.minecraftforge.fml.common.Mod;
import de.keksuccino.fancymenu.api.visibilityrequirements.VisibilityRequirementRegistry;

@Mod("modid")
public class ExampleModMainClass {

    public ExampleModMainClass() {
        try {

            //Register your VisibilityRequirement to the VisibilityRequirementRegistry at mod init.
            VisibilityRequirementRegistry.registerRequirement(new ExampleVisibilityRequirementWithValue());

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```