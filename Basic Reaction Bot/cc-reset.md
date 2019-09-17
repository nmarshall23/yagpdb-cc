# reset

## Trigger Type:

Command

## Trigger:

trig

## Response:

```
{{/* */}}
{ const := (sdict
    "dbPrefix" "test"
    "actionMsgkey" "test--actionMsgId"
    "emoji" (cslice "" "" "")
    "userValueDbPrefix" "test--user|"
    "userPattern" "test--user|%"
    "cc" (sdict
      "update" 0
      "reset" 0
    )
  )
}}

{{/*_______*/}}

{{ $myUserId := (toInt64 0) }}
{{ $dbkey := "BossFight--voteMsgId" }}

{{$embed := cembed
"title" "__Boss Invasion__"
}}

{{ $retId := sendMessageRetID nil $embed }}

{{ addMessageReactions nil $retId "🕕" "🕖" "🕗" "🕘" }}

{{ dbSet (toInt64 0) $const.actionMsgkey (toString $retId) }}

{{ deleteTrigger 20 }}
```

## Aditional Notes:
