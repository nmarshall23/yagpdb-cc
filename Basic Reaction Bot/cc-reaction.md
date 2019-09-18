# Command Name

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
    "userValueDbPrefix" "test--user|R"
    "userPattern" "test--user|%"
    "cc" (sdict
      "update" 0
      "reset" 0
    )
  )
}}

{{/*__Filter Out Bot__*/}}

{{if not (eq .Reaction.UserID .ReactionMessage.Author.ID) }}
  {{ $dbkey := (joinStr "" $const.userValueDbPrefix .Reaction.Emoji.Name) }}

  {{/*__Add or Remove__*/}}

  {{if .ReactionAdded }}

    {{/*__Set Data__*/}}

    {{ $data := (userArg  .Reaction.UserID).Username }}
    {{ dbSet .Reaction.UserID $dbkey $data }}
  {{else}}
    {{ dbDel .Reaction.UserID $dbkey }}
  {{end}}

  {{ scheduleUniqueCC $const.cc.update nil 1 0 (sdict ) }}
{{end}}
```

## Aditional Notes:
