# Constants

```
{{ $d := (sdict
    "dbPrefix" "bossInv"
    "channel" "boss-invasion-signup"
    "emoji" (cslice "🕕" "🕖" "🕗" "🕘")
    "keys" (sdict
      "voteMsgId" "bossInv--voteMsgId"
      "userVotePrefix" "bossInv--user|"
      "bossName" "bossInv--name"
    )
    "cc" (sdict
      "update" 37
      "reset" 36
      "sendReminder" 24
    )
    "role" (sdict
      "org" 622604425076277249
    )
  )
}}
```
