---
description: Guide to customizing XP requirements
---

# XP Requirements

The amount of XP required to level up skills can be configured in the `xp_requirements.yml` file.

## Expressions and Variables

Within a section, such as the `default` section, you will see an `expression` value that contains the expression/equation used to calculate the XP requirements.

The expression can be changed as you wish, but it must be a valid EvalEx expression. You can view the supported operators and functions [here](https://github.com/uklimaschewski/EvalEx#supported-operators).

{% hint style="info" %}
The result of the expression will always be rounded to the nearest whole number
{% endhint %}

Variables are also supported in expressions. In order to have a different XP required for each level, you must have the `level` variable in the expression somewhere. This variable corresponds to the level that is unlocked upon reaching the required XP. The `level` starts at 2 and goes up to the maximum level of the skill. For example, the result of the expression when `level` is 5 is the XP need to go from level 4 to 5.

Custom variables are also supported, which allow you to label and organize the parts of your expression. Instead of using the numbers directly in the expression, you can turn it into a variable that is specified in its own key. In the default expression shown below, `multiplier` and `base` are examples of custom variables.

```text
multiplier * (level - 2) ^ 2 + base
```

As you can see, the numeric values of `multiplier` and `base` are specified as keys with the same name as the variable:

```text
default:
  expression: 'multiplier * (level - 2) ^ 2 + base'
  multiplier: 100.0
  base: 100.0
```

You can use any variable name, as long as the value of the variable is defined in a separate key of the same name.

## Skill Overrides

You can create different XP requirements for each skill by adding a `skills.[skillName]` section that will override the `default` section. The keys and values in the skill section are the same as the `default` section.

Here is an example of Alchemy XP requirements that override the default:

```text
default:
  expression: 'multiplier * (level - 2) ^ 2 + base'
  multiplier: 100.0
  base: 100.0
skills:
  alchemy:
    expression: 'multiplier * (level - 2) ^ 3 + base'
    multiplier: 20.5
    base: 20.0
```

