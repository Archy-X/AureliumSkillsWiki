---
description: Guide to configuring and customizing GUI menus
---

# Menus

Menus in Aurelium Skills are inventory GUIs that display information about skills to players in-game. This includes personal skill and stat menus, skill progression, ability descriptions, Some menus are accessible by commands, such as /skills and /stats, while others are accesible by clicking buttons in other menus.&#x20;

Since the Menu Update significantly changed configuration format and added new features, this guide is applicable to Aurelium Skills version Beta 1.3.0 and newer. If you are upgrading from an earlier version and are already familiar with the old format, see the [changes from the legacy format](menu-format-changes.md) first.

## File structure

The files for configuring menus are located in the `AureliumSkills/menus` folder. Each menu has its own corresponding file used to configure that menu.

### Placeholders

Much of the menus file uses placeholders, which is text surrounded by `{` and `}`. When the menu is actually opened, the placeholder will be replaced by the corresponding message in the messages file. The path of the placeholder message is found under either the `menus.common` or `menus.[menu_name]` section with either the same or similar key as the placeholder.

However, some placeholders are more generic ones that are not found in the menus section of the messages file. For example, the `{skill}` placeholder is replaced with the name of a skill.

It is recommended to make any changes to the actual text context of menus in the corresponding message in the messages file in order to preserve multi-language support. Any change to the text in a placeholder will make it no longer work.

### Menu keys

The following is a list of keys and sections that are at the left-most indentation of the file (referred to here as the menu section).

* `title` - The text that will show up at the top of the menu when it is opened
* `size` - The number of rows the menu has, from 1-6 (each row has 9 slots)
* `fill` - A section used to define the menu background item to fill empty slots, see .
* `items` - The main items section used for singular items
* `templates` - The section used to define items with custom contexts and multiple instances
* `options` - A section found in some menu files that contains custom options and settings

### Fill item

The `fill` section defines a background item to fill empty slots not used by other items. There are two required keys in the `fill` section:

* `enabled` - A true/false value of whether the fill item should be used
* `material` - The material of the fill item

The display name of a fill item is automatically turned into a space, so the name of the item is invisible. Additional keys can be added to customize item meta using the same format as other items (see ).

### Items section

The `items` section is used to define singular items in the menu. Each subsection is the unique name of the item, which is used as a unique key. The item names that exist in the default menus are reserved words, meaning that items with those names have functionality or placeholders used by the plugin. Custom items can be added using any non-reserved name in the `items` section using the same format as other items. See adding custom items for additional information.

### Templates section

The templates section is used for items with multiple instances or contexts, such as each skill item in the skills menu. Template items usually have the same lore and display name for all contexts, with differences applied internally through placeholders. Each context in a template, which is a specific type such as each skill, has its own subsection within the template to define any differences for that context only. The following example shows the basic structure of a template:

```
templates: # The templates section
  skill: # The skill template
    farming: # The context for farming
      pos: ... # Keys in this section only apply to the farming item
      material: ...
    foraging: # Another context for foraging
      pos: ...
      material: ...
    # Any key that is not the name of a context applies to all contexts of the item 
    display_name: ... # Applies to all contexts
    lore: ... # Applies to all contexts
```

Since templates are only used for items already defined by default, custom templates cannot be created.

## Items

Items refers to sections in both the `items` and `templates` sections, as most keys apply to both. There are two required keys for all items and most templates:

* `material` - The material of the item, such as `dirt` or `diamond`. See below for details.
* `pos` - The position/slot of the item on the menu, either in the comma separated `row,column` format or as a single slot number from 1-53. See below for details.

### Material

The material field is required on all items and most templates and defines the type of the item. In Minecraft 1.13+, the proper name of a material can be found in game by hovering over an item in the inventory with advanced tooltips enabled (F3 + H). The dark gray text on the bottom after `minecraft:` is the name of the material used in menu configuration. Lowercase is recommended but capitals are also allowed.

In Minecraft 1.12, some items have an additional data value (a number) that must be used to define some items such as different colors of stained glass or wool and different types of logs. This data value is added to the material name in the `material:data` format. For example, `log:2` defines a birch log. Data values can be seen in game with advanced tooltips as the number after a # in the item display name. The data value of 0 does not have to be defined.

In templates, the material is either defined in a context subsection or the main item section. Materials defined in a context will only apply to that specific context, while a material defined in the main section will be the default material if no context-specific material is defined.

### Pos

The `pos` key on items is the position or slot on the menu the item is located. There are two acceptable formats for `pos`:

#### Row,column format

This format is defined as `row,column`, such as `2,3` for the second row and the third column. The first row and column starts at 0. Row can be from 0-5 and column can be from 0-8. Row 0 is the top-most row and column 0 is the left-most column.

#### **Slot format**

This format is a single number from 0-53 indicating the slot number of the item. 0 is the top-left slot and the number increases left to right, then top to bottom.

### Display Name and Lore

The `display_name` key contains the text used for the item display name. Color codes and placeholders are supported.

The `lore` key is a list of strings containing the lore displayed on the item. Color codes and placeholders are also supported.

The display name and lore keys also contain built-in placeholders in a `{placeholder}` format. These are replaced internally to display functional parts of the menu. The messages usually correspond to a message with a similar key in the `menus` section of the messages file.

#### Hex Colors

Hex colors are supported in display names and lore using the `&#000000` format or using the [MiniMessage](https://docs.adventure.kyori.net/minimessage/format.html) format.

### Item meta

There are many keys available to define different types of optional item meta. These keys are added in the section of the the item, not in the `material` field but on the same indent level.

#### Enchantments

The `enchantments` key is a list of strings with each entry in the format `name level`, such as:

```
enchantments:
  - sharpness 5
  - unbreaking 3
```

The name of the enchantment is the name used by the vanilla game.

#### Potion data

The `potion_data` section contains subkeys for defining data on a potion. There are three keys in the `potion_data` section:

* `type` - The name of the potion type, such as `speed` or `night_vision`. The type must be a valid Bukkit PotionType (listed [here](https://helpch.at/docs/1.18/org/bukkit/potion/PotionType.html)).
* `extended` - An optional true/false value of whether the potion should have an extended duration (defaults to false).
* `upgraded` - An optional true/false value of whether the potion should have an upgraded level (defaults to false).

An example of a potion\_data section with all three keys:

```
potion_data:
  type: night_vision
  extended: true
  upgraded: true
```

#### Custom effects

The `custom_effects` section is a map list defining custom potion effects on a potion (this is different from potion data). Each object in the map list must have three keys:

* `type` - The type of potion effect to use, must be a valid Bukkit PotionEffectType (listed [here](https://helpch.at/docs/1.18/org/bukkit/potion/PotionEffectType.html)).
* `duration` - The duration of the potion effect, in ticks (20 ticks = 1 second).
* `amplifier` - The level of the potion effect, with an amplifier of 0 being level 1.

Below is an example of a `custom_effects` section with multiple custom effects (Fire Resistance I for 10 seconds and Haste II for 30 seconds):

```
custom_effects:
  - type: fire_resistance
    duration: 200
    amplifier: 0
  - type: fast_digging
    duration: 600
    amplifier: 1
```

#### Item flags

The `flags` key is a list of item flags to add to the item. Item flags are a type of meta used to hide other meta on the item from being shown to the player. Below is a list of valid flags and the format used in item configuration:

```
flags:
  - hide_attributes
  - hide_destroys
  - hide_dye
  - hide_enchants
  - hide_placed_on
  - hide_potion_effects
  - hide_unbreakable
```

#### Glow

The `glow` key is a true/false value that adds the glowing enchantment effect to the item without showing the enchantment name if set to true. It is equivalent to adding an enchantment and a hide\_enchants item flag.

#### Skull meta

The `skull_meta` section can be used to add a custom skin texture to a player head item. The section must have one of three possible sub-keys, `uuid`, `base64`, or `url`.

The `uuid` key is the UUID of the player's skin texture to use. The `base64` key is a base64 string of the texture. The `url` is the minecraft.net URL containing the texture.\


Below is an example of using skull meta. You only need ONE of the three options.

```
skull_meta:
  uuid: 6302a69e-9995-4f95-b2cd-d37b8ab875c9
  base64: eyJ0ZXh0dXJlcyI6eyJTS0lOIjp7InVybCI6Imh0dHA6Ly90ZXh0dXJlcy5taW5lY3JhZnQubmV0L3RleHR1cmUvNjIxMTk3ZTUzYzFhYjExMmU2ODA3OWQzYzgzZmE0NzE0Yzc3YTgzZDA2MjFhMjlkNzYyZTk5ZTlmZWFhZTRkNSJ9fX0=
  url: http://textures.minecraft.net/texture/621197e53c1ab112e68079d3c83fa4714c77a83d0621a29d762e99e9feaae4d5
```

#### Durability

The `durability` key sets the durability of the item from 0 to the max durability of the item (a value of 0 means the item is almost broken).

#### NBT

NBT data can be added to an item using the `nbt` section. This section supports nested NBT structures and will automatically detect the type of data inputted.&#x20;

#### Item registry keys

The `key` key can be used in an item section to use an item in the item registry. Any item can be registered in game using `/skills item register`. This is used instead of defining `material` and other meta. This can be convenient when an item has already been created in game or is too complex.

## Click Actions

Click actions are used to define custom functionality when a player clicks an item in the menu. This includes executing a command, closing the menu, opening another menu, and more.

### Triggers

There are multiple ways click actions can be triggered (key in parenthesis):

* Any click (`on_click`)
* Left click (`on_left_click`)
* Right click (`on_right_click`)
* Middle click (`on_middle_click`)
* Drop key (`on_drop`)

The trigger key is used to name the section that contains the click actions for that particular trigger. For example, all the actions under an `on_click` section will be activated when the player clicks that item with any mouse button.

### Types

Once you have created a section under the item with a trigger name, click actions are defined underneath using [map list](../rewards.md#yaml-syntax) syntax.

Each action must have a `type` defined, either `command` (executing a command) or `menu` (menu navigation).

#### Command

For command actions, an `executor` (either `console` or `player`) and the `command` itself must be defined. Commands with a `console` executor will be run through console, while a `player` executor will be run as if the player had typed it (accounts for player permissions too).&#x20;

The `command` text should not include the beginning slash. It supports PlaceholderAPI placeholders and a built in placeholder of `{player}` (player username).

#### Menu

Menu actions are for anything related to menu navigation. You must define the specific action type using the `action` value, which can be as follows:

* `open` - Opens another menu (must be within the Aurelium Skills plugin)
* `close` - Closes the current menu
* `next_page` - Moves to the next page of the menu, if applicable
* `previous_page` - Returns to the previous page of the menu, if applicable

The `open` action type also requires a `menu` value, which is the internal name of the menu to open (this is usually the lowercase name with spaces replaced with underscores).

The `open`, `next_page`, and `previous_page` action types also take an optional `properties` section that is used to define menu behavior, though this option is hard to use unless you dig through the source code.

### Examples

Command action activated on any click that executes a command through console:

```
some_item:
  on_click:
    - type: command
      executor: console
      command: say hi
```

Menu action activated on right click only that closes the menu:

```
some_item:
  on_right_click:
    - type: menu
      action: close
```

Multiple click actions under the same trigger (will activate together):

```
some_item:
  on_click:
    - type: command
      executor: player
      command: shop
    - type: command
      executor: console
      command: say Player opened shop
```

## Custom Menu Items

Completely new items can be added to menus by simply defining a new section in the `items` section with the name of your new item. The custom item name cannot be the name of an existing built-in item.&#x20;

The format of the custom item is the same as any other item (material, pos, display\_name, lore, etc). Click actions and PlaceholderAPI placeholders are also supported.
