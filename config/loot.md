---
description: Guide to configuring loot tables
---

# Loot

## Overview

The Fishing and Excavation skills have abilities that can drop custom loot, which is configured in the `loot` folder. For Fishing, the `treasure_hunter` ability corresponds to the rare pool and the `epic_catch` ability gives items from the epic loot pool. The `metal_detector` ability in Excavation gives rare loot while the `lucky_spades` ability gives epic loot.

{% hint style="info" %}
The drop chances for the abilities are configured separately in `abilities_config.yml`, see the [Abilities](abilities.md) page for more details.
{% endhint %}

Beyond changing the items dropped for these abilities, the files enable adding custom loot pools unrelated to abilities, executing commands as loot, as well as creating new loot tables for other skills (Foraging and Mining).

## File Structure

Loot tables are separated into files for each skill in the loot folder. The name of the file is the skill that the file corresponds to. By default, there are excavation and fishing loot tables. You can optionally add loot tables for mining and foraging, as long as they follow the format.

## Loot Pools

Loot pools are lists of loot entries, and each loot table file can have multiple loot pools. In the default excavation and fishing loot tables, there are the rare and epic loot pools. However, you can add any amount of new loot pools.

Loot pools are defined in the pools section of the loot file. Each pool must have a unique name for the config section name. In excavation and fishing, `rare` and `epic` are reserved names that integrate with abilities, so it is discouraged to change them.

Keys:

* `base_chance` - The chance to select this pool without any added ability bonuses (1 = 1% chance) (defaults to 1)
* `selection_priority` - The order the pools are potentially selected, a higher priority means that it will attempt to select before lower priority pools (defaults to 1)
* `override_vanilla_loot` - Whether the regular loot from the block should be replaced with the selected loot. Does not apply to fishing (defaults to 1).
* `chance_per_luck` - The amount the chance of selecting the pool should increase by per Luck stat level the player has (0.1 = +0.1% chance per Luck) (defaults to 0)
* `require_open_water` - For Fishing, only give items in the pool when the player fishes in open water (5x5x5 volume of water) when set to true. This prevents giving loot when using most AFK fish farms (defaults to false).

Each pool has a loot section containing a map list of the loot entries. This uses the same type of syntax as rewards, which is explained [here](https://wiki.aurelium.dev/skills/config/rewards#yaml-syntax).

## Loot Entries

Currently, there are two types of loot: item loot and command loot. Each loot entry must have certain required keys and can optionally have more. Optional keys are either notated with (optional) or have their default values specified on this page. Each key is explained below:

Universal Keys (apply to any loot type):

* `type` - The type of loot, either `item` or `command`
* `weight` - The weight of the entry compared to other loot in the same pool. A higher weight means the loot entry is more likely to be selected (defaults to 10).
* `message` - A chat message to send to the player when they get the loot. This supports color codes and PlaceholderAPI (optional).
* `sources` - A list of sources or source tags that this loot should exclusively apply to. The names of sources should match the exact name in sources\_config.yml. Does not support custom block sources yet (optional).
* `xp` - The amount of skill xp to give when this loot is dropped (defaults to the original source amount)

### Item Loot

Item loot keys:

* `material` - The material of the item, must be valid bukkit material name (not case sensitive). Use material:id to specify legacy data if on 1.12
*   `amount` - Controls the amount of item to give. This can either be a single number like '5' or a range of numbers such as '1-5', which gives a random amount from 1 to 5 (both inclusive) (defaults to 1)


* `key` - References an item key registered using /skills item register. If this is specified, material and all keys below do not apply
* `display_name` - The display name of the item, supports & for color codes unless escaped with \\& (optional)
* `lore` - The lore of the item, must be a list of each line, supports & for color codes unless escaped with \\& (optional)
* `enchantments` - A list of enchantments, one enchantment per line. Use a space between the enchantment name and the level, such as 'sharpness 5' (optional)
* `potion_data` - A section containing potion data, see below for keys (optional):
  * `type` - The type of potion, must be a bukkit PotionType
  * `extended` - Whether the potion has an extended duration
  * `upgraded` - Whether the potion has an upgraded level
* `custom_effects` - A map list of effects, keys for each section below (optional):
  * `type` - The name of the effect, must be a bukkit PotionEffectType
  * `duration` - The duration of the effect, in ticks
  * `amplifier` - The amplifier of the effect (0 means level 1)
* `glow` - Set to true to make the item glow without enchantments showing (optional)
* `nbt` - Section for any custom NBT data (optional)
* `flags` - List of item flags to add to the item (optional)
* `ignore_legacy` - If true, the plugin will skip loading the item if the server version is below 1.13 to prevent material parsing errors. The only reason you should use this if you are planning on using the same config for legacy and modern versions and an item you have does not exist in 1.12. The plugin is able to recognize modern material names on legacy versions without any issues. (optional)

#### Examples

Basic example of an item loot:

```
- type: item
  material: iron_ingot
  weight: 10
  amount: 1-3
```

Here is a more complex example with display name, lore, and enchantments:

```
- type: item
  material: diamond_sword
  weight: 5
  amount: 1
  display_name: '&cFire Sword'
  lore:
    - '&7Powerful weapon'
    - ' '
    - '&9RARE'
  enchantments:
    - sharpness 5
    - fire_aspect 2
    - looting 3
```

Here is a potion with base potion data and custom effects:

```
- type: item
  material: potion
  weight: 10
  amount: 1
  potion_data:
    type: speed
    upgraded: true
  custom_effects:
    - type: jump
      duration: 1000
      amplifier: 2
    - type: regeneration
      duration: 40
      amplifier: 3
```

An item with hidden enchants using item flags and custom model data using the nbt section

```
- type: item
  material: paper
  weight: 10
  amount: 1
  nbt:
    CustomModelData: 14
  enchantments:
    - knockback 2
  flags:
    - hide_enchants
```

### Command Loot

Command loot is used to execute any command when the player gets the loot, either through console or by the player.

Command loot keys:

* `executor` - Who should execute the command, either console or player (defaults to console)
* `command` - The command without the beginning /, supports {player} placeholder and all PlaceholderAPI placeholders

Example:

```
- type: command
  weight: 10
  executor: console
  command: say hi
```

## Loot Selection

The way loot is selected is fairly straightforward:

1. The loot table is determined by skill that corresponds to the action the player does. For block based loot, the block must be a source for a supported skill (foraging, mining, excavation).
2. A loot pool is selected from the loot table starting from the highest priority loot pool. Whether pool is selected is base on the pool's base\_chance and any added chances. If a pool is not selected, the pool with the next highest selection priority will be attempted. If no loot pool gets selected, the below steps do not apply.
3. A single loot entry is selected from the pool based on the weight of the entry. A higher weight makes it more likely for it to be selected. The exact chance is calculated by `weight / sum of all weights in pool`.

