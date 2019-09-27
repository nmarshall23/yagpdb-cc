# reset

## Trigger Type:

Command

## Trigger:

trig

## Response:

```
{{/*__SET__ __Const__*/}}
<<Insert const here! $d />>

{{/********/}}

{{/*__Del__ __Old__ __Values__*/}}
{{with $db := (dbGet (toInt64 0) $d.keys.voteMsgId) }}
  {{ deleteMessage $d.channel $db.Value 1 }}
{{end}}

{{ range (dbGetPattern (toInt64 0) (joinStr "" $d.dbPrefix) 10 0) }}
  {{ dbDel .UserID .Key }}
{{ end }}

{{ range (dbTopEntries (joinStr "" $d.keys.userVotePrefix "%") 60 0) }}
  {{ $pattern := (split .Key "|") }}
  {{ $name := index $pattern 1 }}
  {{ takeRoleID .UserID ($d.role.Get (joinStr "" "seeking" $name)) }}
  {{ dbDel .UserID .Key }}
{{ end }}




{{/*__New__ __Msg__*/}}
{{ $embed := cembed "title" "__Stand by__ *Reseting*" }}
{{ $msgId := sendMessageRetID nil $embed }}

{{range $k, $v := $d.emoji }}
  {{ sleep 1 }}
  {{ addMessageReactions nil $msgId $v }}
{{end}}

{{dbSet (toInt64 0) $d.keys.voteMsgId (toString $msgId) }}


{{if .Message.ID }}
  {{ deleteTrigger 3 }}
{{end}}

{{ execCC $d.cc.update $d.channel 1 (sdict )}}
```

## Aditional Notes:
