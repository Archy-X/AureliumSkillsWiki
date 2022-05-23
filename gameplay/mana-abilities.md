---
description: Explanation and descriptions of mana abilities
---

# Mana Abilities

## What are mana abilities?

Mana Abilities are a special type of ability that costs mana to use and are active, meaning they require the player to activate or use. Currently, this is the primary use of mana. Mana Abilities are by default unlocked at level 7 of that skill and increase in level every 7 levels (This is configurable). Level increases can change duration/power, cooldown, and mana cost. (These are all configurable in abilities\_config.yml)

Using Mana Abilities will give Sorcery XP.

## How do players see Mana Abilities?

Mana Abilities are not visible in the main skills menu until the player unlocks it at level 7. After unlocking it, hovering over the skill item will show the mana ability name, level, duration/power, cooldown, and mana cost. Players can see mana abilities they haven't unlocked yet in the level progression menu at levels of a multiple of 7. Those items will display a description of the mana ability and the duration/power of it at that particular level.

## List of mana abilities

Replenish (Farming) - Replants crops automatically for a certain duration. Right-click with a hoe and break a crop to activate. Works with wheat, carrots, potatoes, nether wart, and beetroot.

Treecapitator (Foraging) - Breaks entire trees instantly for a certain duration. Right-click with an axe and break a log to activate. Works best with oak, birch, and spruce trees (One block wide). The algorithm is not final and will be improved later on to work perfectly with all tree types.

Speed Mine (Mining) - Gives Haste 10 for a certain duration. Right-click with a pickaxe and break stone or an ore to activate.

Sharp Hook (Fishing) - Deal damage to a hooked entity when left-clicking with a fishing rod'

Terraform (Excavation) - Break blocks instantly in a 4 block radius in the same layer when digging. You must use a shovel and extra blocks broken must be the same type and in a single connected vein. Right click shovel and dig block to activate.

Charged Shot (Archery) - Arrows you shoot will deal more damage based on how far the bow was pulled back, consuming mana in the process. Does more damage per mana consumed. Left click a bow to toggle charged shot mode.

Absorption (Defense) - Incoming damage will decrease mana by 2x Minecraft damage instead of your health. Mana will not regenerate while Absorption is active. Left click shield and take damage to activate.

Lightning Blade (Fighting) - Increases attack speed by _% for_ seconds. Right click sword and attack mob to activate.

## How do I disable mana?

Mana can be essentially disabled through a few steps:&#x20;

1\. Set all the `mana_cost` and `mana_cost_per_level` to `0` in `abilities_config.yml` under the `mana_abilities` section. This is the only thing required to functionality disable mana.&#x20;

2\. Remove mana from the action bar by editing the messages under `action_bar` in the messages files. You may want to consider disabling the action bar entirely in `config.yml` under `action-bar`.&#x20;

3\. Rename messages to remove mentions of mana. For example, Mana Ability could be renamed to Active Ability or similar. Most of the messages that mention mana are in the `menus` section of the messages files. You would also want to remove mentions of mana cost and rename level up messages in the `leveler` section.
