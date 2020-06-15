# Constants
This is a dictionary of common constants used by all of the commands in boss invasion.
 
You will have to customize it and add it to each of the commands.


Notes:

`$d.channel` is the name of the channel that contains the reaction msg.

`$d.emoji` these are emoji reactions for voting.

`$d.cc` command ids for update, reset sendReminder commands.

`$d.role` role Id. A reminder is send to this role. 

```
{{ $d := (sdict
    "dbPrefix" "bossInv"
    "channel" "reminders-signup"
    "emoji" (cslice "🕕" "🕖" "🕗" "🕘")
    "keys" (sdict
      "voteMsgId" "bossInv--voteMsgId"
      "userVotePrefix" "bossInv--user|"
      "bossName" "bossInv--name"
    )
    "cc" (sdict
      "update" 1
      "reset" 2
      "sendReminder" 3
    )
    "role" (sdict
      "org" 626963911727513601
    )
  )
}}
```
