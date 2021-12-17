---
description: Guide to configuring abilities and mana abilities
---

# Abilities

## Basic

Abilities are perks and buffs that you unlock and level up as you level up skills. Each skill has a maximum of 5 abilities. If a skill does not have any abilities, then the abilities for that skill have not been added yet. Abilities are usually passive, meaning they do not require any extra player input to activate or use. For active abilities, see [**Mana Abilities**](https://github.com/Archy-X/AureliumSkills/wiki/Mana-Abilities).

To see your ability levels easily, hover over an item in the skills menu (/skills). If an ability name is dark gray and crossed out, that means you have not unlocked that ability yet. To see the descriptions for what each ability does, hover over the items in the level progression menu, which is seen by clicking on any skill item in the skills menu. Each skill level shows what abilities are unlocked/leveled up at that skill level with descriptions.

To allow for the leveling of abilities, each ability has one or two **values**. This value(s) determines how powerful the ability is depending on the level. This could be a percentage chance, percent extra damage, etc. When dealing with percentages in the config, you should use the percent as the value in the config (0-100).

## Using abilities\_config.yml

The abilities\_config.yml is a new file in version Alpha 1.6.0.

The file is split into 2 main sections, `abilities` and `mana_abilities`.

### abilities

This section contains the options for the regular, passive abilities. Each ability is split into sections by their skill.

The options:

* `enabled` - Whether this ability should be enabled. If set to false, the ability will be hidden from menus or messages and will not function.
* `base` - The base value of the ability at level 1 (see above for what values are). If the ability has 2 values, this is the first one displayed in the default English description.
* `per_level` - This is how much the value should increase **per ability level**. The formula for the value of ability at a given level is `value = base + ((level - 1) * per_level)` where `level` is the level of the ability, not the skill.
* `unlock` - This is the skill level the ability should unlock at. The default is from 2-6, depending on the ability.
* `level_up` - This is the multiple the ability levels up at (every x levels the ability should level up). If an ability has a `level_up` of 3, it would level up every 3 skill levels. Defaults to 5.
* `max_level` - The maximum ability level. Setting this value to 0 allows infinite levels. Keep in mind that an ability level cannot exceed what the maximum skill level allows. This value should be below the max skill level to have any effect naturally. This will still apply if you use commands to set your skill level above the max. Defaults to 0.

Other options:

* `base_2` - The second base value of the ability at level 1. This is the second one displayed in the default English description.
* `per_level_2` - The same as per\_level, but for the second value.
* Some abilities have specific options and are fairly self-explanatory.

### mana\_abilities

This section contains the options for the active abilities that use mana.

The options:

* `enabled` - Whether this mana ability should be enabled. If set to false, the mana ability will be hidden from menus or messages and will not function.
* `base_value` - The base value of the mana ability at level 1. Values work the same as abilities but are usually in the context of durations or percents.
* `value_per_level` - This works the same as per\_level for normal abilities.
* `cooldown` - The base cooldown of the ability for the mana ability at level 1, in seconds. This can be a decimal.
* `cooldown_per_level` - The time the cooldown should increase/decrease per mana ability level. If the value is positive the cooldown will increase per level, if it is negative the cooldown will decrease per level.
* `mana_cost` - The base mana cost of the mana ability at level 1.
* `mana_cost_per_level` - How much the mana cost should change per mana ability level.
* `unlock` - This controls the level the mana ability unlocks at. Defaults to 7.
* `level_up` - This is the multiple the mana ability levels up at (every x levels the mana ability should level up).
* `max_level` - The maximum mana ability level. It works the same as max\_level for regular abilities.

Other options:

* `require_sneak` in replenish, treecapitator, speed\_mine, and terraform - If set to true, the player must be sneaking (shifting) to raise their pickaxe.
* `display_damage_with_scaling` in sharp\_hook - Whether the damage displayed in the menu should use the hp\_indicator\_scaling.
* `enable_sound` in sharp\_hook and charged\_shot - Whether the sound should be played when the player attacks with Sharp Hook and Charged Shot
* `enable_particles` in absorption - Whether a pink circle of particles should show when damaged with Absorption activated.
* `check_offhand` in replenish, treecapitator, speed\_mine, and terraform - If set to true, the tool will not be raised if the player right clicks with a block in their offhand that they placed (such as torches).
* `sneak_offhand_bypass` in replenish, treecapitator, speed\_mine, and terraform - If set to true, sneaking will disable the offhand check and will always raise the tool.
* `enable_message` in charged\_shot - Whether a chat message should be sent when firing a bow with Charged Shot.
* `max_blocks_multiplier` in treecapitator - Scales the number of blocks broken by this value
