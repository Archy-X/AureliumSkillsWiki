---
description: List of menu config format changes in Beta 1.3.0 from older versions
---

# Menu Format Changes

This is a detailed list of the configuration format changes in Beta 1.3.0 from versions before Beta 1.3.0. Existing configurations will migrate automatically, but any new changes made after updating must be done in the new format.

## List of changes

* The existing menus.yml has been replaced by individual files for each menu in the new menus folder.
  * Existing changes to menus.yml will be automatically migrated to the new files.
    * Exception: the lore of the rank item in the level progression menu will be reset due to new additions to it.
  * The old menus.yml has been renamed to menus-OLD.yml and should not be used. This is just a backup of your menu config before it was migrated.
* The `rows` menu entry has been renamed to `size`. The value of `size` functions the same as `rows` (1-6).
* Material names are now in lowercase (though uppercase is still allowed).
* The `row` and `column` entries for items has been replaced with the `pos` entry with two acceptable formats:
  * The `row,column` format, such as `3,0` for row 3, column 0 (the first row/column is always 0)
  * The `slot` format, which is a single number for the slot number from 0 up to 53 (starting at the top left slot increase left to right then top to bottom)
* Each context (every skill/stat that has a different material/position) in a template has been moved to its own subsection under the template name.
  * Values such as the material, pos, and item meta of each context are separate fields under the subsection with the context name.
  * The following is an example of the new format for contexts in templates:

```
templates:
  skill:
    farming: # The subsection with the name of the context
      material: diamond_hoe # The material for the farming context
    foraging: # A different subsection for foraging
      material: stone_axe
```

* Item meta options, such as potion\_data, are now separate fields under the item section (alongside material, lore) for items and in the context subsection for templates.
  * The `material` field is just for the material name and not for any item meta (glow, potion\_data, nbt, etc).
  * The following is an example of item meta being defined in the new format:

```
items:
  rank: # The name of the item
    material: paper # Only contains the material name
    potion_data: # Separate subsection for potion data
      type: instant_heal # Some item meta options require additional subsections
```

* Legacy material data for 1.12 is still defined in the material field, using the material:data format
