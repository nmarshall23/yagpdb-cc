# mkVoteMsg

## Trigger Type:
Command

## Trigger:
mkVoteMsg

## Response:
```
{{ $myUserId := (toInt64 509925858270642206) }}
{{ $dbkey := "BossFight--voteMsgId" }}

{{$embed := cembed 
"title" "__Boss Invasion__" 
}}

{{ $retId := sendMessageRetID nil $embed }}

{{ addMessageReactions nil $retId "🕕" "🕖" "🕗" "🕘" }}

{{ dbSet $myUserId $dbkey (toString $retId) }}

{{ deleteTrigger 20 }}

```

## Aditional Notes:
