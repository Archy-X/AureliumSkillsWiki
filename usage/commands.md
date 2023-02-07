---
description: List of plugin commands
---

# Commands

Syntax: `[this]` indicates a required argument, `(this)` is an optional argument. See [Permissions](https://github.com/Archy-X/AureliumSkills/wiki/Permissions) for more details about permissions.

## Skill Commands

Aliases: `/sk`, `/skills`, `/skill`. Any command that says /sk works with all the aliases.

`/sk` - Opens the skill menu

### XP Commands

`/sk xp add [player] [skill] [amount] (silent)` - Gives Skill XP to a player in a certain skill

`/sk xp set [player] [skill] [amount] (silent)` - Sets a player's skill XP for a certain skill to an amount

`/sk xp remove [player] [skill] [amount] (silent)` - Removes skill XP from a player in a certain skill

### Leaderboard Commands

`/sk top (page)` or `/sk top [skill] (page)` or `/sk top average (page)` - Shows the top players in a skill (Alias: `/skilltop`)

`/sk rank` - Shows your skill rankings (Alias: `/skillrank`)

### Skill Commands

`/sk skill setlevel [player] [skill] [level]` - Sets a specific skill to a level for a player

`/sk skill setall [player] [level]` - Sets all of a player's skills to a level

`/sk skill reset [player] (skill)` - Resets all skills or a specific skill to level 1 for a player

### Modifier Commands

`/sk modifier add [player] [stat] [name] [value] (silent) (stack)` - Adds a stat modifier to a player. Setting `silent` to true will not send a feedback message. Setting `stack` to true will add the stat modifier even if the `name` is already used by appending a number to the end.

`/sk modifier remove [player] [name] (silent)` - Removes a specific stat modifier from a player

`/sk modifier list (player) (stat)` - Lists all or a specific stat's modifiers for a player

`/sk modifier removeall (player) (stat) (silent)` - Removes all stat modifiers from a player

`/sk item modifier add [stat] [value] (lore)` - Adds an item stat modifier to the item held, along with lore by default

`/sk item modifier remove [stat] (lore)` - Removes an item stat modifier from the item held, and the lore associated with it by default

`/sk item modifier list` - Lists all item stat modifiers on the item held

`/sk item modifier removeall` - Removes all item stat modifiers from the item held

`/sk armor modifier add [stat] [value] (lore)` - Adds an armor stat modifier to the item held, along with lore by default

`/sk armor modifier remove [stat] (lore)` - Removes an armor stat modifier from the item held, and the lore associated with it by default

`/sk armor modifier list` - Lists all item armor modifiers on the item held

`/sk armor modifier removeall` - Removes all armor stat modifiers from the item held

### Requirement Commands

`/sk item requirement add [skill] [level] (lore)` - Adds an item requirement to the item held, along with lore by default

`/sk item requirement remove [skill] (lore)` - Removes an item requirement from the item held, and the lore associated with it by default

`/sk item requirement list` - Lists the item requirements on the item held

`/sk item requirement removeall` - Removes all item requirements from the item held

`/sk armor requirement add [skill] [level] (lore)` - Adds an armor requirement to the item held, along with lore by default

`/sk armor requirement remove [skill] (lore)` - Removes an armor requirement from the item held, and the lore associated with it by default

`/sk armor requirement list` - Lists the armor requirements on the item held

`/sk armor requirement removeall` - Removes all armor requirements from the item held

### Miscellaneous Commands

`/sk lang [language]` - Changes your player language

`/sk multiplier (player)` - Shows a player's current XP multiplier based on their permissions

`/sk abtoggle` - Toggles your own action bar

`/sk help` - Shows help page

### Profile Commands

`/sk profile skills [player]` - Views the skill levels of another player. `player` is the username of the player you want to view skills for. This player does not have to be online.

`/sk profile stats [player]` - Views the stat levels of another player.

### Admin Commands

`/sk save` - Saves skill data

`/sk updateleaderboards` - Updates and sorts the leaderboards

`/sk reload` - Reloads the config, messages, menus, loot tables, action bars, boss bars, and health and lucks stats.

`/sk transfer [playerFrom] [playerTo]` - Copies the player data from one player to another. `playerFrom` and `playerTo` must be valid UUIDs. The player data from `playerFrom` is not reset. Players do not have to be online for this to work.

`sk resethealth` - Removes all AureliumSkills player health and luck attributes. Useful if you are uninstalling the plugin. This command can only be run through console and there should be no players online to work properly.

### Backup Commands

`/backup save` - Saves a backup of the current skill data to the backups folder.

`/backup load [file]` - Loads a backup from the backups folder. You must specify the exact file name, including the file extension. This will override the current skill data, so it is advised to take a backup before loading one.

### Mana Commands

`/mana (player)` - Shows how much mana you or another player has

`/mana add [player] [amount] (allowOverMax) (silent)` - Adds mana to a player

`/mana remove [player] [amount] (silent)` - Removes mana from a player. Mana cannot go below 0, any extra is ignored.

`/mana set [player] [amount] (allowOverMax) (silent)` - Sets the mana of a player.

## Stats Commands

`/stats` - Opens the stats menu

## Skill Name Commands

`/[skill]` - Opens the level progression menu directly for a specific skill, can be enabled/disabled in config (ex: /farming, /archery, /healing)

## Item Registry Commands

`/sk claimitems` - Opens the unclaimed items menu to claim unclaimed items

`/sk item register [key]` - Registers the held item to a unique key

`/sk item unregsiter [key]` - Unregisters an item

`/sk item give [player] [key] (amount)` - Gives a registered item to a player. If the player does not have enough inventory space, the item will be added to the player's unclaimed items.
