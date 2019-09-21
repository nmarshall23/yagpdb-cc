# Constants

```
{{ $const := (sdict
    "dbPrefix" "bossInv"
    "channel" "boss-invasion-signup"
    "emoji" (cslice "🕕" "🕖" "🕗" "🕘")
    "key" (sdict
      "voteMsgId" "bossInv--voteMsgId"
      "userVotePrefix" "bossInv--user|"
      "bossName" "bossInv--name"
    )
    "cc" (sdict
      "update" 0
      "reset" 0
      "sendReminder" 24
    )
  )
}}
```
