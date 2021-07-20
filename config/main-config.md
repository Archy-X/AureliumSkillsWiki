---
description: Guide to the config.yml file
---

# Main Config

This is a guide to the `config.yml` file found in the `plugins/AureliumSkills` folder.

If an option you see in the config is missing, this page may not have been updated yet or the option may have been removed. You can find any config additions and changes in the full plugin [changelog](https://github.com/Archy-X/AureliumSkills/blob/master/Changelog.txt).

Last Updated Version: `Beta 1.1.4`

## General

### MySQL

`mysql:`

* `enabled` - Whether MySQL should be used for data storage \(requires a restart to enable\)
* `host` - MySQL hostname
* `port`- Port \(must be number\)
* `database` - Database name \(must be created already\)
* `username` - MySQL username
* `password` - MySQL password
* `load-delay` - Number of ticks to delay loading data after a player joins, useful for syncing multiple servers to a single database
* `always-load-on-join` - If true, player data will always be loaded from the database when a player joins, regardless if it is already in memory
* `ssl` - Whether to use SSL

### Languages

`default-language` - The default language for players; must have a file that matches \(ex: `messages_en.yml` for `en`\)

`try-detect-client-language` - If set to `true`, the plugin will try to use the client's language, if available and valid. This is only for players who have not set a language using commands, or if their language was reset after a server restart. If the client language is not a valid plugin language, it will use the `default-language`. If set to `false`, all unset players will use the `default-language`.

`languages` - A list of languages players can switch to using `/skills lang <language>`; must also have a file that matches. Custom language files are defined here.

### Action Bar

`action-bar:`

* `enabled` - Whether the action bar should be enabled/disabled \(Must be set to `true` to have any action bars; setting to `false` disables all action bar types\)
* `idle` - Controls the idle action bar \(not gaining xp\). **Enable this if you want the action bar to always display.**
* `ability` - Controls the action bar for ability messages \(raise/lower, activate, etc.\). If set the false, the ability messages will be sent through chat instead.  
* `xp` - Controls the action bar for gaining xp \(not maxed\)
* `maxed` - Controls the action bar when xp is gained in a maxed skill
* `update-period` - How often the action bar should update, in ticks \(Increase this value if action bar is causing lag\)
* `round-xp` - If enabled, current xp will be rounded to an integer.
* `placeholder-api` - Whether PlaceholderAPI placeholders should be replaced in the action bar, given that you have PlaceholderAPI

### Boss Bar

`boss-bar:`

* `enabled` - Whether boss bars should be enabled for xp gains
* `mode` - Can be either `single` or `multi`. `multi` means multiple boss bars will display if gaining XP from different types of skills, `single` is only one at a time.
* `stay-time` - How long the boss bar should stay up after not gaining xp, in ticks
* `update-every` - Controls how often the boss bar should update when gaining xp consecutively, increase if having lag issues
* `round-xp` - If enabled, the current xp will be rounded to an integer.
* `format` - The format list allows you to change the boss bar color and style for each skill:
  * Format: '\[SKILL\] \[COLOR\] \[STYLE\]'
  * Available colors are BLUE, GREEN, PINK, PURPLE, WHITE, RED, and YELLOW
  * Available styles are SOLID, SEGMENTED\_6, SEGMENTED\_10, SEGMENTED\_12, and SEGMENTED\_20

`base-mana` - The base amount of mana players should have at 0 Wisdom

`enable-roman-numerals` - Whether Roman numerals should be used for skill levels

### Damage Holograms

`damage-holograms` - Enable/disable damage holograms \(requires HolographicDisplays\)

`damage-holograms-scaling` - Whether the damage displayed on holograms should be scaled according to `health.hp-indicator-scaling`

`damage-holograms-decimal:`

* `display-when-less-than:` - Display decimals in damage holograms when less than a specified damage
* `decimal-max-amount` - The maximum amount of decimal digits to display

`damage-holograms-offset:`

* `x` - X coordinate offset
* `y` - Y coordinate offset
* `Z` - Z coordinate offset
* `random`:
  * `enabled` - Whether random hologram positions should be enabled
  * `x-min` - Minimum X coordinate offset
  * `x-max` - Maximum X coordinate offset
  * `y-min` - Minimum Y coordinate offset
  * `y-max` - Maximum Y coordinate offset
  * `z-min` - Minimum Z coordinate offset
  * `z-max` - Maximum Z coordinate offset

### Leaderboards

`leaderboards:`

* `update-period` - How often leaderboards should be updated, in ticks
* `update-delay` - How long after server startup should the leaderboards be updated, in ticks \(does not include the immediate update on startup\)

## **Gameplay**

`skill-level-requirements-multiplier` - Changes the equation that calculates xp level requirements; defaults to 100 \(`XpRequired = Multiplier * (level - 2) ^ 2 + 100`\)

`enable-skill-commands` - Whether skill name commands should be enabled such as `/farming` or `/mining` \(Requires restart to have an effect\)

`check-block-replace` - Whether blocks placed by players should not give xp; keep `true` unless you are having plugin compatibility issues

### Worlds and Regions

`blocked-check-block-replace-worlds` - Worlds on this list will not be checked for block replaces, allowing placing and breaking of blocks to gain xp.

`blocked-check-block-replace-regions` - WorldGuard regions on this list will not be checked for block replaces \(requires 1.13+\).

`blocked-worlds` - Players in worlds on this list will not be able to gain xp naturally in any skill.

`blocked-regions` - Players in regions on this list will not be able to gain xp naturally in any skill \(requires 1.13+\).

`disabled-worlds` - Most of the plugin's gameplay functionality will be disabled in worlds on this list, including but not limited to stats, abilities, gaining xp, and the action bar \(commands and menus will still be available\)

`disable-in-creative-mode` - Whether players should not be able to gain xp while in creative mode

### Economy

`skill-money-rewards:`

* `enabled` - Whether players should gain money for leveling up skills \(requires Vault\)
* `base` - The base amount of money players gain at level 2
* `multiplier` - The multiplier \(`money = base + multiplier * level * level`\)

### Leveler

`leveler:`

* `title:`
  * `enabled` - Whether a title should be displayed to players on skill level up
  * `fade-in` - Title fade in time, in ticks
  * `stay` - How long the title should last, in ticks
  * `fade-out` - Title fade out time, in ticks
* `sound:`
  * `enabled` - Whether a sound should be played to players on skill level up
  * `type` - The name of the sound that should be played \(must be a valid sound name\)
  * `category` - The sound category the sound should be played in
  * `volume` - Sound volume
  * `pitch` - Sound pitch
* `double-check-delay` - The level up check delay for large xp gains at once, in ticks \(lower is faster\)

### Modifier

`modifier:`

* `armor:`
  * `equip-blocked-materials` - A list of blocks that should not grant stats of armor when right-clicked; add to this list when stats are given but armor is not equipped.
* `item:`
  * `check-period` - How often, in ticks, the item held in a player's hand should be checked for stat item modifiers \(increase if you have lag\)
  * `enable-off-hand` - Whether stat modifiers should work in the off hand
* `auto-convert-from-legacy` - Whether the old modifier nbt format should be converted to the new one. Set to false if you are having performance issues and all your items have been converted.

### Requirement

`requirement:`

* `item:`
  * `prevent-tool-use` - Whether block breaking should be blocked when a player does not meet a requirement
  * `prevent-weapon-use` - Whether attacking entities should be blocked when a player does not meet a requirement
  * `prevent-block-place` - Whether block placing should be blocked when a player does not meet a requirement
  * `global` - Define item requirements that should apply to every item of that type. Format: - '\[material\] \[skill\_1\]:\[level\_1\] \[skill\_2\]:\[level\_2\] ...'
* `armor:`
  * `prevent-armor-equip` - Whether armor should be unable to be equipped when a player does not meet a requirement
  * `global` - Define armor requirements that should apply to every item of that type. Format: - '\[material\] \[skill\_1\]:\[level\_1\] \[skill\_2\]:\[level\_2\] ...'

### Critical

`critical:`

* `base-multiplier` - The base damage multiplier for critical hits
* `enabled` - Options in this category control whether that item type should be able to deal critical hits. \(`hand` is for empty fist, `other` is for holding any other item not on the list\)

### Menus

`menus:`

* `placeholder-api` - Whether PlaceholderAPI placeholders should be used in menus.

### Miscellaneous

`check-for-updates` - Whether the plugin should check for new updates on startup and when a player with the `aureliumskills.checkupdates` permission joins

`automatic-backups:`

* `enabled` - Whether automatic backups should be taken on server shutdown
* `minimum-interval-hours` - The minimum interval, in hours, between automatic backups. Automatic backups will only be taken at least this amount of hours after the last one.

## Skill Options

**All Skills Options**

* `enabled` - Whether this skill should be enabled. Disabled skills will be invisible from menus and unable to be leveled. The abilities and mana abilities of disabled skills will not work.
* `max-level` - The max level obtainable naturally for this skill
* `check-cancelled` - An option on most skills that controls whether block break events should be checked for cancellation \(only disable if there are plugin compatibility issues\)

**Archery and Fighting Options**

* `damage-based` - Option to grant XP every time a player attacks per damage dealt instead of killing the mob. WARNING: This still uses the values in sources\_config.yml as the XP granted PER VANILLA DAMAGE for each type of mob. You should significantly lower and equalize the archery and fighting values in sources\_config.yml if you want to keep the progression similar to before.
* `spawner-multiplier` - Option to change the XP gained from mobs spawned from spawners. Set to 0 to disable XP from mob spawners; set to 1 to match regular mobs \(1 by default\). The XP gained is the spawner-multiplier value multiplied by the XP a normal mob of that type would give.

**Defense Options**

* `max` - The maximum amount of XP that can be gained at once
* `min` - The minimum amount of XP/damage required to gain any XP
* `allow-shield-blocking` - Allow Defense XP gain when blocking with a shield \(false by default\)

**Endurance Options**

* `xp-gain-period` - How often Endurance XP should be gained, in ticks

**Alchemy Options**

* `give-xp-on-takout` - Alchemy option to reward XP when the potion is taken out of the brewing stand.

## Stat Options

### Health

`health:`

* `modifier` - How much vanilla hp should be given for every Health level \(2 = 1 vanilla heart\). By default it is 0.5, which means players will gain half of half a heart \(0.25 of a heart\) for every Health level. This is not affected by `hp-indicator-scaling`.
* `health-scaling` - If enabled, hearts are scaled at high enough hps \(purely visual\), maxing out at 20 hearts. \(This option is to prevent hearts taking up a large portion of the screen, however this means that 1 heart at low hps will not be worth the same as 1 heart at high hps\)
* `hp-indicator-scaling` - How much vanilla hp should be multiplied by for display on the action bar and menus \(Does not affect actual health, purely visual\)
* `update-delay` - How many ticks the plugin should wait before updating health on world switches \(keep at 0 unless you are having plugin compatibility issues\)
* `force-base-health` - If enabled, base health will be forced to 20 every time health updates \(only enable if you are having plugin compatibility issues\)
* `hearts` - This section is used to change the hearts shown for different health ranges. The key is the number of hearts and the value is the minecraft health that amount of hearts is unlocked at. 

  For example, if two entries are '12': 29 and '13': 37, this means the player will have 12 hearts shown on their screen when their minecraft health is from 29 \(inclusive\) to 37 \(exclusive\).

  The values are not the HP shown on the action bar. To find the HP from the action bar the value is, multiply it by the health.hp-indicator-scaling option \(default is 5\).

  This supports hearts below 10 and hearts above 20, just add entries with the key as the number of hearts.

  The order of keys and values should be sequential, otherwise higher heart entries will override lower ones.

  This is purely cosmetic, changing these options does not change the actual hp you have.

  This only works if you have health.health-scaling set to true.

### **Strength**

`strength:`

* `modifier` - How much vanilla damage should be added for every Strength level \(2 = 1 vanilla heart of damage\). If use-percent is set to true, the new damage is `damage = originalDamage * (1 + (strength * modifier) / 100)`. 
* `hand-damage` - Whether strength should work on fists and items that aren't tools or weapons\)
* `bow-damage` - Whether strength should apply for bows
* `display-damage-with-health-scaling` - Whether the Strength descriptors in the stats menu should display damage with `health.hp-indicator-scaling`
* `use-percent` - Whether strength should be calculated on a percentage basis, rather than adding. This will make the base damage more important so waiting for the attack cooldown and using a better weapon will be more important. If this is true, the recommended modifier is 0.63.

### **Toughness**

`toughness:`

* `new-modifier` - Controls the power of the Toughness stat in reducing damage \(See [this](https://github.com/Archy-X/AureliumSkills/wiki/Stats-Information-and-Calculations) for more info\)

### **Regeneration**

`regeneration:`

* `custom-regen-mechanics` - Whether custom regeneration mechanics should be enabled \(allows the control of regen delays but doesn't feel as vanilla\)
* `base-regen` - The base amount of vanilla health regenerated when Regeneration is 0
* `saturated-modifier` - How much addition health should be regenerated per Regeneration level when the player has saturation
* `hunger-full-modifier` - How much additional health should be regenerated per Regeneration level when the player is at full hunger but does not have saturation
* `hunger-almost-full-modifier` - How much additional health should be regenerated per Regeneration level when the player is above 14 hunger points but below 20
* `custom-regen-options:`
  * `saturated-delay` - How fast health should regenerate when the player has saturation, in ticks, if `custom-regen-mechanics` are enabled
  * `hunger-delay` - How fast health should regenerate when the player does not have saturation, in ticks, if `custom-regen-mechanics` are enabled
* `mana-modifier` - How much additional mana should be regenerated per second per Wisdom level
* `base-mana-regen` - The base amount of mana regenerated when Regeneration is 0

### **Luck**

`luck:`

* `modifier` - How much luck attribute should be given per Luck level
* `double-drop-enabled` - Whether the luck double drop functionality is enabled
* `double-drop-modifier` - The chance modifier for double drop per Luck level
* `double-drop-percent-max` - The maximum percent chance for double drops

### **Wisdom**

`wisdom:`

* `anvil-cost-modifier` - The anvil XP cost reduced per Wisdom level
* `experience-modifier` - The increase in vanilla experience gain per Wisdom level
* `allow-over-max-mana` - Whether mana should stay when the Wisdom stat decreases so that the max mana goes below the current mana
* `max-mana-per-wisdom` - How much the max mana should increase per wisdom level

