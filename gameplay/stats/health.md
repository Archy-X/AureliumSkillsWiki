---
description: Detailed guide to health options
---

# Health

Health increases the max HP of the player. It works by adding an AttributeModifier to the GENERIC\_MAX\_HEALTH attribute. It is applied on PlayerJoinEvent, health stat changes, and config reloads.

## Calculation

Health is calculated based on the Health stat level:

`GENERIC_MAX_HEALTH = 20.0 + (Stat.HEALTH * health.modifier)`

Where Stat.HEALTH is the Health Stat Level visible with /stats and health.modifier is the config option `health.modifier` (Default value 0.5)

A `health.modifier` of 1.0 means that every Health Stat level increases the player's HP by 1.0

## Health Scaling:

If `health.health-scaling` is set to true, the amount of hearts displayed on the player's screen is affected by their max health, preventing a player's health from blocking their entire screen. This means that the amount of hearts the player sees will not be 1 heart = 2 HP if their health is greater than 20.0

The amount of hearts displayed on the screen can be customized in the config under the `health.hearts` section of config.yml. The key is the number of heart, and the value is the Minecraft health that amount of hearts is unlocked at. For example, if two entries are '12': 29 and '13': 37, this means the player will have 12 hearts shown on their screen when their Minecraft health is from 29 (inclusive) to 37 (exclusive).

This supports hearts below 10 and hearts above 20, just add entries with the key as the number of hearts. The order of keys and values should be sequential, otherwise, higher heart entries will override lower ones.

This is purely cosmetic, changing these options does not change the actual hp you have, and it only works if you have `health.health-scaling` set to true.

## HP Indicator Scaling

HP Indicator Scaling is the amount the player's raw attribute health should be multiplied by to get the displayed HP on the action bar. It is changed through the config option `health.hp-indicator-scaling`. The default value of 1 makes it so that the action bar HP matches the Minecraft HP (20 HP on action bar = 20 HP in Minecraft). This is also cosmetic and does not affect the actual amount of health a player has.
