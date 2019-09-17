# Basic Reaction Bot

A Reaction bot is a embed message that uses emoji's as a button, then reactions to that.
Due to how YAGPDB reaction trigger for custom commands works, you should use dedicated channels.

Reaction bots are made up of the same basic custom commands.
In this directory contains the template files for creating a new one.

## Overview

These are the custom commands that make up a Reaction Bot.

- interval.md
- reset.md,
- reaction.md,
- update.md

## Database Values

Commands use a prefix for all database values. This lets us use pattern search to find values on users.
The reaction message Id is stored in a DB values with the key `${prefix}-actionMsgId`

## Constants

A dictionary of constants values.

- Database keys, and patterns.
- Reaction emoji
- custom command ids

### reset

Action Msg maintenance and initialization

1. Deletes old reaction message.
2. Removes old database values for this bot from global user aka `userId 0`.
3. Removes old database values from users using pattern search `${prefix}-%`, because `dbTopEntries` can only retrieve up to 100 entries at a time, might need to loop it. Depending on how many user db entries this Reaction bot has.
4. Create a new initial mostly empty embed reaction message store that msgId.
5. Add reaction emoji
6. exec `CC-Update`

### update

Update Action Msg.

1. retrieves any custom values used in Action Msg.
2. retrieves any user values used in Action Msg.
3. create full embed reaction message, fills in values.
4. retrieve reaction message Id
5. edits message

### Reaction

This command uses the Reaction Trigger type.

1. filter out bot's adding of reaction emoji.
2. retrieve reaction message Id, only act on that message Id.
3. If add reaction
   Add user reactions to database `$const.userValueDbPrefix`
   Else remove reaction from database
4. schedule Update msg after a 1 sec, this lets the update be interrupted thus run less often.
   `scheduleUniqueCC $const.cc.update 1 0 nil`

### interval.md

Optional used if the bot automaticly resets every day. or has time based actions.
If it does reset every day, This command executes the reset command.

### Set Value Command
