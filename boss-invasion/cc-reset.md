# reset

## Trigger Type:

Command

## Trigger:

trig

## Response:

```
{{/*__SET__ __Const__*/}}
{{/* Insert const here! */}}


{{/*__Del__ __Old__ __Values__*/}}
{{with $const }}
  {{with $msgId := (dbGet (toInt64 0) .key.voteMsgId) }}
   {{ deleteMessage .channel $msgId.Value 0 }}
  {{end}}

  {{ range (dbGetPattern (toInt64 0) (joinStr "" .dbPrefix "%") 10 0) }}
    {{ dbDel .UserID .Key }}
  {{ end }}

  {{ range (dbTopEntries (joinStr "" .key.userVotePrefix "%") 60 0) }}
    {{ dbDel .UserID .Key }}
  {{ end }}
{{end}}

{{/*__New__ __Msg__*/}}
{{with $const }}
  {{ $embed := cembed "title" "__Stand by__ *Reseting*" }}

  {{ $msgId := sendMessageRetID nil $embed }}

  {{range $k, $v := .emoji }}
    {{ addMessageReactions nil $msgId $v }}
  {{end}}

  {{dbSet (toInt64 0) .key.voteMsgId (toString $msgId) }}


  {{if .Message.ID }}
    {{ deleteTrigger 3 }}
  {{end}}

  {{ execCC .cc.update .channel 3 nil }}
{{end}}
```

## Aditional Notes:
