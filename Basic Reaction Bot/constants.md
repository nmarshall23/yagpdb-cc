# Constants

```
{{ $const := (sdict
    "dbPrefix" "test"
    "actionMsgKey" "test--actionMsgId"
    "channel" "test-channel"
    "emoji" (cslice "" "" "")
    "userValueDbPrefix" "test--user|"
    "userPattern" "test--user|%"
    "keys" (sdict
      "ex1" "test--kEx1"
    )
    "cc" (sdict
      "update" 0
      "reset" 0
    )
  )
}}
```
