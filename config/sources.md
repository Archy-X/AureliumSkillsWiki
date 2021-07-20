---
description: Guide to configuring XP sources
---

# Sources

This is a guide to using and configuring the `sources_config.yml` file.

## Basic Configuration

The sources config is where you configure the amount of skill XP each block, action, mob, etc. should give. The `sources_config.yml` file is divided into sections for each skill.

The key for each source is the name of the source and should not be modified. The value is the amount of skill XP that the source should give by default \(without any modifiers or multipliers\). After changing values, make sure to run `/skills reload` to have them take effect.

## Custom Blocks

The Farming, Foraging, Mining, and Excavation sections support custom blocks \(blocks that are not defined by default\).

To add custom blocks, add a `custom:` section under the specific skill section. In the custom section, the keys are the block name and the values are the XP amount. For example: `blue_concrete: 10.0`

The blocks you add are checked for block replacement by default, meaning players cannot place and break them repeatedly to gain XP. The block names to use are the 1.13+ block names, even if your server is 1.12.

Here is a full example of a custom block for the Mining skill:

```text
sources:
  mining:
    custom:
      sandstone: 4.0
```

## Custom Mobs

**Note: Custom Mobs and MythicMobs support has been removed since Beta 1.1.1, see update changelog for more info.**

The sources config supports custom mobs for Fighting and Archery using MythicMobs.

Just like custom block XP sources, add the "custom:" section under fighting and archery in "sources\_config.yml". Under the section, the keys are the MythicMobs mob internal name and the value is the xp amount. Mob names are case sensitive!

Killing a MythicMob that is defined in the sources config will override the default value for that mob type. Killing a MythicMob that has not been defined in the sources config will give the default xp for that mob type.

Here is a full example of a custom mob for the Archery skill:

```text
sources:
  archery:
    custom:
      SkeletalKnight: 200.0
```

