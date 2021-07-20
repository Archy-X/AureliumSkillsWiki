---
description: Guide to configuring loot tables
---

# Loot

This page is a guide to configuring the `loot.yml` file.

## Sections

Each section corresponds to a specific ability, and will only be used when the corresponding ability activates.

* `fishing-rare` - Treasure Hunter ability in Fishing
* `fishing-epic` - Epic Catch ability in Fishing
* `excavation-rare` - Metal Detector ability in Excavation
* `excavation-epic` - Lucky Spades ability in Excavation

## Basic Format

The basic format for each section is as follows:

`- [minimum amount] [maximum amount] [material]`

The minimum and maximum amounts indicate how much of the item should drop each time that item is chosen. Each entry in a single section has an equal and random chance of being chosen. The number of items to drop indicated by min and max is also randomly chosen from the range. Amounts support 0.

The material name to enter depends on the version of your server. If you are on **version 1.13 or higher**, you enter the standard name of the item seen at the bottom of an item when you have advanced tooltips enabled \(F3+H\). The material name is not case sensitive, but the convention is upper case.

If you are on **version 1.12**, material names may be different than vanilla, see [here](https://helpch.at/docs/1.12.2/index.html?org/bukkit/Material.html) for a list. Additionally, some items may have an item id in addition to the material name \(such as colored wool\). Item ids may be seen at the top right of the item \(with advanced tooltips enabled\) and are the number after the `/` \(the number should be a fairly small number generally between 0 and 15\). If you don't see a slash near the end of the item name then it does not need an item id. Materials with item ids are formatted such as `WOOL:15`, separated by a colon.

### Advanced Format

After the material name in an entry, items support arguments for customizing the item and adding special data. Each argument is separated by a space, thus you cannot have spaces within an argument. Color codes using `&` are supported. In order to follow YAML format, single or double quotes are sometimes required around an entry. Current arguments are limited but consist of the following:

* `name` - This modifies the display name of the item seen in game. Use underscores to replace spaces. Ex: `name:&cFire_Sword`
* `lore` - This adds lore \(extra text under the name\) to the item. Each line of lore is separated by `|`. Use underscores to replace spaces. Ex: `lore:line_1|line_2|line_3`
* `glow` - This option will make the item have an enchantment glint without the item having any visible enchants. \(Adds Protection 1 but is invisible\). Usage: `glow:true`
* `enchantments` - Add enchantments to the item using this option. Each enchantment is formatted `[enchant]:[level]`. Multiple enchants are separated by `|`. Generally, any common enchantment name \(Vanilla or Bukkit names\) will work but use upper case. Example of a single enchantment: `enchantments:PROTECTION:4`. Example of multiple enchantments: `enchantments:PROTECTION:4|SHARPNESS:5|FIRE_ASPECT:2`.

Here is an example of a full entry with many arguments:

`- 1 1 DIAMOND_SWORD name:&cFire_Sword lore:&7Powerful_weapon|_|&9RARE enchantments:SHARPNESS:5|FIRE_ASPECT:2|LOOTING:3`

## Commands

Instead of using items as loot table entries, you can also use a command. Commands will be run through console. Commands MUST have their own entry, you cannot have both an item and command on the same line.

Format: `- cmd:[command]`

The `[command]` does NOT contain a `/` and **does** support spaces. Note: You might need to wrap it around single quotes like this: `- 'cmd:say hi'`.

You can use the `{player}` placeholder to replace the username of the player who activates the ability.

