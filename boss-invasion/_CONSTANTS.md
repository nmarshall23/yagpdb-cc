# Constants

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
