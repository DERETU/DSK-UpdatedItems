
# Installation

1. Download updatedItems.sk
2. Put the downloaded file in the 'plugins/Skript/scripts/DeretuSkript/' Folder (Without '')
3. Make sure you have installed Skript v2.11.1 or later (https://github.com/SkriptLang/Skript)
4. Make sure you have installed SkBee v3.11.2 or later (https://github.com/ShaneBeee/SkBee)
5. Make sure you have installed skUtilities v0.9.2 or later (https://tim740.github.io/)
6. Restart the server or reload the Skript using /sk reload
7. Run '/updatedItems info' to make sure the script was installed correctly


# What is Updated Items?

This script is a tool for server owners. It allows you to save and update certain items so that every player has the same version. This way, you can easily make changes to items, which then get automatically refreshed for all players.

For example, your server has a sword named "Slayer" which you can buy in a shop. The sword is a netherrite sword enchanted with sharpness 7.
After opening the shop you however realize that sharpness 7 is to strong, so you want to change it to sharpness 5. The problem: People already have the old sword with sharpness 7, and you would have to manually remove it from them or code something that does the job.
This script makes the job way easier, as you would be able to simply run "/ui save <id>" with the new item in hand and then update it with "/ui update <id>"!
More information on how this works and how to set it up is below.


# Why use Update Items?

This script is very easy to use, but still powerful and can save a lot of time and effort when used correctly.
It comes with very natural commands and full tab completion support.
It is easy to integrate into other projects and compatible with other scripts.
And the script is completely free to use and open source. Read the information for developers at the bottom of the readme if you are planning on changing things in the code.

Personally, I always found it very annoying to not have this script, so I hope I can help others to not have the same issue!


# Commands & Permissions

/updatedItems [/ui] (dsk.updatedItems.command): Basic command
/ui save (dsk.updatedItems.save): Save an item
/ui savedTags/savedLore/savedDurability/savedUnbreakable/savedName (dsk.updatedItems.save): Change the preserved values for an item
/ui give (dsk.updatedItems.give): Give an item
/ui remove (dsk.updatedItems.remove): Remove an item
/ui update (dsk.updatedItems.update): Release/Update an item
/ui info: Get information on the script
/ui reload (dsk.updatedItems.reload): Reload the scripts configuration
/ui list (dsk.updatedItems.list): List all items


# More Detailed explanation below

# Creating a new item

To create a new item, simply run "/ui save <id>" while holding the item in hand. The id will later be used to change the item.
Additionally, you should do "/ui update <id>" to make sure that the item gets updated. This is technically not needed, as this item does not have a previous version.


# Updating an item

Updating an item is as simple as running "/ui save <id>" while holding the new item.
However, in order for other players to get their items refreshed, you have to run the command "/ui update <id>", called "releasing". This will make it so whenever a player joins, closes their inventory or picks up an item, their inventory will be searched for items that are "out of date". These items will then be replaced with their new versions.
For performance reasons, chests and shulker boxes will not be searched by the script. It only ensures that the items in a players inventory are up to date and that they can't use an item that isn't up to date. I might consider adding an option to enable searching containers in the future.


# Removing an item

To remove an item, simply do "/ui remove <id>". This will NOT delete the items in the inventory of players.
This functionality will be added as an option in the future, though I probably would not recommend using it. This is because to make sure the old items don't appear again, you would have to permamently save all deleted items.


# Giving an item

To give yourself an item, use "/ui give <id>". You can add true or false to the end of the command. True makes it so you get the released item, while false gives you the newest version.


# Preserving values for items

Sometimes you do not want EVERY single part of an item to be cleared. This could include things like nbt, durability or lore.
An example for this could be a sword with a kill counter. Whenever a player gets killed, it adds 1 to a counter in the swords nbt and puts that number into the lore of the item. Now, you don't want the counter to reset whenever the item gets updated, so you add the line in the lore and the nbt tag to the saved values of the item.
Saved values do not update, so they are permament. You can always change them to refresh again though.
There are 5 types of saved values (more coming in future updates):
 - SavedTags saves nbt data. Simply use "/ui savedTags <id> <action>" to add/remove/clear/list tags. Note that the actual nbt tag will be "minecraft:custom_data;<your tag>" and not just "<your tag>".
 - SavedLore saves certain lines of an items lore. Use "/ui savedLore <id> <action>" to add/remove/clear/list lines.
 - SavedUnbreakable saves the unbreakable state of items.
 - SavedDurability saves the durability state of items. This is true by default, which I recommend. Otherwise, items with durability would constantly switch to the same value after being used, which you probably don't want.
 - SavedName saves the name of the items. Could be used for something like an xp counter in the item's name.


# Listing items

You can list all created items with "/ui list <released/unreleased/all>". 
Listing all items will display unreleased items in red and released items in green. Clicking the "give" button will follow the default settings for giving released/unreleased items.
Listing unreleased items will display all items that could possible receive an update. Clicking the "give" button will give the unreleased item.
Listing released items will display all items that have been released at some point. This can also include unreleased items. Clicking the "give" button will give the released item (the one that players currently have).


# Blacklist updating

Sometimes you don't want to get items updated for certain people (e.g. it's annoying to get your items updated while trying to make changes). To prevent this, simply set the "dsk.updatedItems.blacklistUpdating" permission to true.


# Information for developers

This script is completely open source and free to use. You can do with it whatever you want, as long as you don't claim it as your own and/or resell/redistribute it without my permission.
I would appreciate if you messaged me that you use this if you do, so I can see that people find it helpful!

If you need any help, you can reach out to me on discord (@deretu). I rarely read my email or github.

The 2 functions in this script are
 - DSK_UpdatedItems_refreshConfig() for refreshing the config
 - DSK_UpdatedItems_refreshItems(player) for refreshing the items in a player's inventory