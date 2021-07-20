---
description: Stats information and calculations
---

# Stats

There are 6 different stats that are upgraded through skills:

## **Health**

Health increases the max HP of the player.

* Adds a AttributeModifier to Attribute.GENERIC\_MAX\_HEATLH
* Applied on PlayerJoinEvent, health stat changes, and config reloads
* How Health is calculated based on stat level:
  * `Attribute.GENERIC_MAX_HEALTH = 20.0 + (Stat.HEALTH * Setting.HEALTH_MODIFIER)`
  * Where Stat.HEALTH is the Health Stat Level visible with /stats and Setting.HEALTH\_MODIFIER is the config option "health.modifier" \(Default value 0.5\)
  * A "health.modifier" of 1.0 means that every Health Stat Level increases player HP by 1.0
* **Health Scaling:**
  * If "health.health-scaling" is set to true, the amount of hearts displays on the player's screen is affected by their max health, preventing a player's health from blocking their entire screen. This means that the amount of hearts the player sees will not be 1 heart = 2 HP if their health is greater than 20.0
  * Health scaling caps at a maximum of 2 full rows of hearts
* **HP Indicator Scaling**
  * Changed through config option "health.hp-indicator-scaling"
  * HP Indicator Scaling is the amount the player's raw attribute health should be multiplied by to get the displayed HP on the action bar.
  * The default value of 5 makes it so that 20.0 raw HP = 100 Displayed Action Bar HP
* See the [Health page](https://wiki.aurelium.dev/skills/stats/health) for more detailed information

## **Strength**

Strength increases the damage a player does in attacks

* Strength is applied on EntityDamageByEntityEvent
* How damage is calculated from strength:
  * `Damage = InitialDamage + (Stat.STRENGTH * Setting.STRENGTH_MODIFIER)`
  * Where Stat.Strength is the Strength Stat Level visible with /stats and Setting.STRENGTH\_MODIFIER is the config option "strength.modifier" \(Default value 0.1\)
* If use-percent is set to true:
  * `Damage = InitialDamage * (1 + (Stat.STRENGTH * Setting.STRENGTH_MODIFIER) / 100)`

## **Toughness**

Toughness decreases the damage dealt by enemy attacks

* Toughness is applied on EntityDamageEvent
* How Toughness is calculated:
  * `Damage = OriginalDamage * (1 - (-1 * (1.01)^(-1 * Stat.TOUGHNESS * Setting.TOUGHNESS_MODIFIER) + 1))`
  * Where Stat.Toughness is the Toughness Stat Level visible with /stats and Setting.Toughness\_MODIFIER is the config option "toughness.new-modifier" \(Default value 1\)

## **Regeneration**

Regeneration increases the natural regeneration rate

* Two options: _Vanilla_ or _Custom_
* **Vanilla**
  * Used when "regeneration.custom-regen-mechanics" is set to false
  * Changes the amount regenerated on EntityRegainHealthEvent if regain reason equals RegainReason.SATIATED
  * If player saturation is greater than 0:
    * `AmountRegenerated = VanillaAmount + (Stat.REGENRATION * Setting.SATURATED_MODIFIER)`
    * Where Stat.REGENERATION is the Stat Level and Setting.SATURATED\_MODIFIER is the config option "regeneration.saturated-modifier" \(Default value 0.05\)
  * If player hunger is full \(20\) but saturation = 0:
    * `AmountRegenerated = VanillaAmount + (Stat.REGENRATION * Setting.HUNGER_FULL_MODIFIER)`
    * Where Stat.REGENERATION is the Stat Level and Setting.HUNGER\_FULL\_MODIFIER is the config option "regeneration.hunger-full-modifier" \(Default value 0.025\)
  * If player hunger is greater than 14 but not full:
    * `AmountRegenerated = VanillaAmount + (Stat.REGENRATION * Setting.HUNGER_ALMOST_FULL_MODIFIER)`
    * Where Stat.REGENERATION is the Stat Level and Setting.HUNGER\_ALMOST\_FULL\_MODIFIER is the config option "regeneration.hunger-almost-full-modifier" \(Default value 0.025\)
* **Custom**
  * Used when "regeneration.custom-regen-mechanics" is set to true
  * Non-saturated regen:
    * Applied every Setting.HUNGER\_DELAY ticks \("regeneration.custom-regen-options.hunger-delay", Default 60\)
    * If player hunger is full \(20\):
      * `AmountRegenerated = Setting.BASE_REGEN + (Stat.REGENERATION * Setting.HUNGER_FULL_MODIFIER`
      * Where Setting.BASE\_REGEN is config option "regeneration.base-regen" \(Default value 1\)
    * If player hunger is greater than 14 but not full:
      * `AmountRegenerated = Setting.BASE_REGEN + (Stat.REGENERATION * Setting.HUNGER_ALMOST_FULL_MODIFIER`
  * Saturated regen:
    * Applied every Setting.SATURATED\_DELAY ticks \("regeneration.custom-regen-options.hunger-delay", Default 20\)
    * `AmountRegenerated = Setting.BASE_REGEN + (Stat.REGENERATION * Setting.SATURATED_MODIFIER`
    * Where Setting.SATURATED\_MODIFIER is config option "regeneration.saturated-modifier" \(Default value 0.05\)
  * Changes to Setting.SATURATED\_DELAY and Setting.HUNGER\_DELAY will only take effect on server restart

## **Luck**

Increase Luck attribute \(better chest and fishing loot\) and chance for double drops

* Modifies Attribute.GENERIC\_LUCK
* `Luck = Stat.LUCK * Setting.LUCK_MODIFIER`
* Setting.LUCK\_MODIFIER is config option "luck.modifier" \(Default value 0.1\)
* Applied on PlayerJoinEvent, luck stat changes, and config reloads
* Chance to give double drops when breaking certain blocks
  * Includes stone, cobblestone, sand, dirt, gravel, grass\_block, andesite, diorite, and granite
  * `% Chance = Stat.LUCK * Setting.DOUBLE_DROP_MODIFIER * 100`
  * Setting.DOUBLE\_DROP\_MODIFIER is config option "luck.double-drop-modifier" \(Default value 0.005\)
  * Maxes out at a chance of Setting.DOUBLE\_DROP\_PERCENT\_MAX \("luck.double-drop-percent-max", default value 100\)

## **Wisdom**

Increases experience gained from any source and decreases anvil costs

* `ExperienceGained = InitialExperience * (1 + (Stat.WISDOM * Setting.EXPERIENCE_MODIFIER))`
* Setting.EXPERIENCE\_MODIFIER is config option "wisdom.experience-modifier" \(Default value 0.01\)
* `NewCost = OriginalCost * (1 - (-1 * 1.025^(-1 * Stat.WISDOM * Setting.ANVIL_COST_MODIFIER) + 1))`
* Setting.ANVIL\_COST\_MODIFIER is config option "wisdom.anvil-cost-modifier" \(Default value 0.25\)

