---
description: Guide to the messages files
---

# Messages

This guide is for using and translating Aurelium Skills messages. Almost all content is translatable, such as commands, menus, and chat.

The messages files can be found in the `messages` folder. Each file corresponds to a different language. Players can select their own personal language using `/skills lang [language]`.

## General Information

### Important Information

* **You must define all the languages you want to use in config.yml** under the "languages" list. This is a list of the two-letter Locale codes that match your file name.
* To change the default language, change the "default-language" in config.yml
* **Do not change any messages placeholders!** Placeholders are text wrapped in { and } \(Ex: {placeholder}\)
* Do not remove newlines \(\n\) in the "menus" section unless your menus.yml format requires it
* **Do not touch the file\_version field**
* **When naming your file, it must be in the format messages\_\[language\].yml** \[language\] must be a valid two-letter Java Locale code or a locale with country code such as messages\_pt-BR.yml

### Important YAML Syntax Tips

* **Never use tabs!** Use correctly aligned spaces instead.
* If your message contains characters "&", "{", or "}", **wrap the entire message in single quotes.** \(Ex: 'Message'\). When in doubt, put it in single quotes.

### General Tips

* Use newlines in descriptions for when the menu item doesn't fit or look good on the screen.
* Unit placeholders can be used everywhere and are changed in the "units" section. To use units in messages, use "{mana\_unit}", "{hp\_unit}", "{xp\_unit}", etc.
* {value} placeholders do not include % symbols.
* If you are creating a new translation, use the template [here](https://github.com/Archy-X/AureliumSkills/blob/master/src/main/resources/messages_template.yml). 
* Be sure to reference [messages\_en.yml](https://github.com/Archy-X/AureliumSkills/blob/master/src/main/resources/messages_en.yml) for the placeholders and format

## Guide to Creating an Offical Translation

This is a guide to creating an official translation to be added to the plugin publicly. Translations here must follow certain format guidelines and rules to be accepted. Any translation that does not follow all the guidelines will have to be revised by the author to be accepted.

It is highly recommended that you translate on [Crowdin](https://crowdin.com/project/aureliumskills). It makes it much easier to edit, collaborate, upload, and download translations. All you have to do is create an account and you can translate! If you do not see your language on the list, please contact Archy in the [Discord](https://discord.gg/Bh2EZfB) to add it. There are also options to upload existing files \(so you don't have to start over\) and to download translations \(so you don't have to wait for a plugin update\) when you click on the 3 dots next to the file in each language section.

### Guidelines

1. Do not change or remove any color codes, keep the same color scheme as the default messages\_en.yml
2. Do not change or remove any newlines \(\n\) in the menus section
3. Do not remove any placeholders that are in the default messages
4. Try to keep translations as accurate as possible. Translations should not affect the meaning of descriptions and names
5. Do not change stat symbols or colors
6. Do not remove any entries in the file; all entries in the default messages must exist in your translation.
7. Do not change action bar, level up title, or level up formats
8. Add newlines \(\n\) in ability, skill, and stat descriptions when you think it is too long. Use your best judgment and test \(if possible\). I will change newlines if necessary.
9. Use the most up to date file found on GitHub
10. Don't translate a language if the translation already exists; add to the existing file if it needs to be updated
11. Keep formats as much as possible, such as punctuation, colors, caps, etc. You may need to move around color codes to get the contexts/parameters to match.
12. The file must be named in the correct format with the correct language code \(If it's wrong it's not a big deal I can fix it myself\)

