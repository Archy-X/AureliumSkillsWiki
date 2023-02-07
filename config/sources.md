---
description: Guide to configuring XP sources
---

# Sources

This is a guide to using and configuring the `sources_config.yml` file.

## Basic Configuration

The sources config is where you configure the amount of skill XP each block, action, mob, etc. should give. The `sources_config.yml` file is divided into sections for each skill.

The key for each source is the name of the source and should not be modified. The value is the amount of skill XP that the source should give by default (without any modifiers or multipliers). After changing values, make sure to run `/skills reload` to have them take effect.

## Custom Blocks

The Farming, Foraging, Mining, and Excavation sections support custom blocks (blocks that are not defined by default).

To add custom blocks, add a `custom:` section under the specific skill section. In the custom section, the keys are the block name and the values are the XP amount. For example: `blue_concrete: 10.0`

The blocks you add are checked for block replacement by default, meaning players cannot place and break them repeatedly to gain XP. The block names to use are the 1.13+ block names, even if your server is 1.12.

Here is a full example of a custom block for the Mining skill:

```
sources:
  mining:
    custom:
      sandstone: 4.0
```
