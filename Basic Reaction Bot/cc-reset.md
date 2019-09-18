# reset

## Trigger Type:

Command

## Trigger:

trig

## Response:

```
{{/*__SET__ __Const__*/}}
{{ $const := (sdict
    "dbPrefix" "test"
    "actionMsgKey" "test--actionMsgId"
    "channel" "test-channel"
    "emoji" (cslice "" "" "")
    "userValueDbPrefix" "test--user|"
    "userPattern" "test--user|%"
    "cc" (sdict
      "update" 0
      "reset" 0
    )
  )
}}

{{/*__Del__ __Old__ __Values__*/}}

{{ $oldretId := dbGet (toInt64 0) $const.actionMsgKey }}
{{ if $oldretId }}
   {{ deleteMessage $const.channel $oldretId.Value 1 }}
{{ end }}

{{ range (dbGetPattern (toInt64 0) (joinStr "" $const.dbPrefix) 10 0) }}
  {{ dbDel .UserID .Key }}
{{ end }}

{{ range (dbTopEntries $const.userPattern 60 0) }}
  {{ dbDel .UserID .Key }}
{{ end }}



{{/*__New__ __Msg__*/}}

{{$embed := cembed
"title" "__Stand by__ *Reseting*"
}}

{{ $msgId := sendMessageRetID nil $embed }}

{{range $k, $v := $const.emoji }}
  {{ addMessageReactions nil $msgId $v }}
{{end}}

{{ dbSet (toInt64 0) $const.actionMsgKey (toString $retId) }}


{{ if .Message.ID }}
  {{ deleteTrigger 3 }}
{{ end }}

{{ execCC $const.cc.update $const.channel 3 nil }}
```

## Aditional Notes:
