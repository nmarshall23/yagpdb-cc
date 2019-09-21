# Command Name

## Trigger Type:

Command

## Trigger:

trig

## Response:

```
{{/*__SET__ __Const__*/}}
<<Insert const here! $d />>

{{/**** LOCAL BOT SETTING */}}
{{/********/}}

{{/*__Filter Out Bot__*/}}

{{if not (eq .Reaction.UserID .ReactionMessage.Author.ID) }}
  {{ $dbkey := (joinStr "" $d.keys.userVotePrefix .Reaction.Emoji.Name) }}

  {{/*__Add or Remove__*/}}

  {{if .ReactionAdded }}

    {{/*__Set Data__*/}}

    {{ $data := (userArg  .Reaction.UserID).Username }}
    {{ dbSet .Reaction.UserID $dbkey $data }}
  {{else}}
    {{ dbDel .Reaction.UserID $dbkey }}
  {{end}}

  {{ scheduleUniqueCC $d.cc.update nil 1 0 (sdict ) }}
{{end}}
```

## Aditional Notes:
