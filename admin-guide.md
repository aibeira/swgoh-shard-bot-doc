# SWGOH Shard-bot Admin Guide
## Getting Started
To begin using the bot, you need to accomplish the following tasks:

1. Add the bot to the server
0. Configure administration role
0. Add players
0. Add payouts

## Add bot to Discord server
Use the following link to add the bot to your Discord server.  You will need to be an administrator, though not the owner, of the server.

https://discordapp.com/oauth2/authorize?&client_id=347564015917989889&scope=bot&permissions=0

When this link is first hit, you will be asked to sign into Discord, if you have not already signed in.  After signing in, select the server to which you want to add the bot and hit the "Authorize" button, as seen here:

![Image](images/add_bot.png)

You may be asked to prove you are not a robot - just confirm that, and the bot will be authorized on your server, as confirmed by Discord like here:

![Image](images/add_bot_success.png)

## Configure adminstration role
After the bot has been added to the server, the bot needs to be configured with one or more Discord roles that contain those Discord users that will administer the bot configuration (player data, payout data, etc...)  This initial configuration can only be completed by the owner of the Discord server.  The command is as follows:

`;cfg adminrole add <admin-role-name>`

**Note:** The `<admin-role-name>` in this command needs to be replaced with the *name* of the Discord role you want to use.

The successful adding of an adminRole to the bot looks like this:

![Image](images/add_adminrole.png)

## Players
Players can be added using the administration web page, once the bot is in the server, and at least one adminRole has been configured, and add players that way.  The admin page url is: 

http://www.mralwerner.com/swgoh-shard/admin

When you access this page, you will be asked ot sign into Discord in order to retrieve a list of servers to allow you to manage the data.  Select the server you want to manage, and then click "Players".

![Image](images/admin_page_main.png)

After accessing the Players page, you will need to click the "Add Player" button at the bottom.

![Image](images/admin_page_player.png)

Fill in the required fields, and hit "Save Player."  

The following fields are required:
 
* **Name** - The player's in-game and/or Discord name.
* **Type** - The player's type - Friend or Enemy
* **Payout Time (UTC)** - The time of the player's payout in the UTC time, and in format "HH:mm" - 24-hour time in the UTC time zone (*no "am/pm" or time-zone should be specified*).  For example, 01:00 is 1:00am UTC, or 9:00pm EDT.   
* **Payout Hour** - The hour component of the player's payout time.  This field will eventually be removed, as it can be derived, but for now, just enter the number of the hour you just put in the payout time UTC.

The other fields are optional.

* **Price** - Informational display of a "price" on an enemy player's head.  Meant to indicate the desire of the allies in the shard to have this player "hit" repeatedly until such time as they give up and stop ruining the allies fun.
* **Payout Rotation** - Indicates the order in a payout rotation for a friendly player.  This is more easily managed in the payouts administration page, after a payout has been created.
* **SWGOH.gg Profile URL** - The link to the player's swgoh.gg profile.  It will be displayed in most places the player's name is displayed in the webpage and in Discord.
* **Discord Emoji** - A Discord Emoji that will be displayed in Discord next to the players name.  It should include the leading and trailing colon (:).  For example ":flag_us:" is the emoji for the US flag and ":poop:" makes a nice emoji to be next to an enemy.

## Adding players using Ally Codes

Players can be added to the bot's data for your shard using the players' ally codes.  This is done using two commands: `;acg` and `;bpa`.

## ally-code-get (`acg`)
The `;acg` command retrieves information about a specific player using their ally code and begins the process of adding that player to the bot's data.  This command must be executed in a channel in the shard's server.  This is completed via direct message exchange with the bot.  That data includes:
* name
* payout time

Usage: `;acg <ally-code>`

Here is an example of it being used in the channel:

![Image](images/acg_channel.png)

Here are exampes of the process continuing through direct message exchange:

![Image](images/acg_dm_1.png)

![Image](images/acg_dm_2.png)

## bulk-player-add (`bpa`)
The `;bpa` command is used to add a players in bulk from an uploaded plain-text list of ally codes.  The type of the players can be specified as enemy or friend on the command, but if omitted, enemy is assumed.

Usage: `;acg [--type friend]`

**Text File Format**

The text file should be a list of ally codes, one per line.  For example:

```
878834387
617334837
911145120
915345238
732421962
755719414
861941268
353829640
673953483
```

The bot will update you on it's progress as it goes through the list.  It is suggested that you not do more than about 50 players at a time.

## Payouts
Payouts can be managed in the admin page.  You can add payouts and edit payouts, including adding players to rotation, reorder the rotation, reverse the order in which rotations rotates, and cycle the rotation.  This page is accessed by clicking the "Payouts" link from the main admin page after logging in:

![Image](images/admin_page_main.png)

The payouts managment page allows for management of payouts data:

![Image](images/admin_page_payout.png)

## Scheduling automatic payout notification
You can schedule the bot to dump into a specific channel the data for a specific payout at a specific time.  This command must be executed in the channel in which you wnat the notification.  The command is:

`;pon --add --utcTime <utcTime> --name <friendly-name>`  

* `<utcTime>` - the HH:mm time for the scheduled notification
* `<friendly-name>` - one of the friendly-names for the payout to be dumped

This example schedules one for 11:30pm UTC:

![Image](images/scheduled_notification.png)

## Discord IDs
* Frequently when dealing with shard-bot or getting support for it, you'll need various Discord IDs - Player IDs, Server IDs, Channel IDs, Role IDs, etc.  Most of these can be found in the Discord clients, if you turn on "Developer Mode" on your user settings:
    * User Settings > Appearance (usually a good portion of the way down the list) > Advanced (near the bottom) section > Developer Mode
* Once Developer Mode is enabled, you can right-click (or tap) on most things and get an option "Copy ID"
* The Server ID can also be found in the Server Settings:
    * Server Settings > Widget > Server ID