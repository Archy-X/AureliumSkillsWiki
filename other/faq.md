---
description: Frequently asked questions
---

# FAQ

### How do I get the action bar with health and mana to always show on the screen?

Set `action-bar.idle` to true in config.yml.

### How do I use mana?

See [https://wiki.aurelium.dev/gameplay/mana-abilities](https://wiki.aurelium.dev/gameplay/mana-abilities)

### Why does it say "Player does not have a Skills profile!" when trying to open the skills menu? / Why are the items in the skills menu missing?

Restart the server. You likely reloaded the server, which is not supported and will break things.

### Will you ever support 1.8?

No. Too much would have to be re-coded and features would be cut.

### Is there a developer API?

Yes, find the dependency info at the bottom of the [README](https://github.com/Archy-X/AureliumSkills). The main class is AureliumAPI, which contains static methods you can use.

### How do I uninstall the plugin and remove extra hearts

To uninstall, put the plugin back and run `skills resethealth` in the console when no players are online. Then immediately remove the plugin and restart.

### **Why are AureliumSkills commands not working on my Minehut server?** 

This is an issue with Minehut's server software, there is nothing I can do on my end to fix it. This issue is not present on normal Spigot/Paper server jars. You can either send them this \([https://pastebin.com/1ZSeFy7K](https://pastebin.com/1ZSeFy7K)\) error that is causing it and hope they fix it or preferably get a proper server host that allows you full file and console access

