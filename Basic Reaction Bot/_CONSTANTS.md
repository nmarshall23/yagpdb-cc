# Constants

```
{{ $const := (sdict
    "dbPrefix" "test"
    "channel" "test-channel"
    "emoji" (cslice "" "" "")
    "keys" (sdict
      "voteMsgId" "test--actionMsgId"
      "userVotePrefix" "test--user|T"
      "ex1" "test--kEx1"
    )
    "cc" (sdict
      "update" 0
      "reset" 0
    )
    "role" (sdict
      "org" 0
    )
  )
}}
```
