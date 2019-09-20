# Command Name

## Trigger Type:

Command

## Trigger:

trig

## Response:

```
{{/*__SET__ __Const__*/}}
{{/* Insert const here! */}}

{{/*__Filter Out Bot__*/}}

{{if not (eq .Reaction.UserID .ReactionMessage.Author.ID) }}
  {{ $dbKey := (joinStr "" $const.key.userVotePrefix "T" .Reaction.Emoji.Name) }}

  {{/*__Add or Remove__*/}}

  {{if .ReactionAdded }}

    {{/*__Set Data__*/}}

    {{ $data := (userArg  .Reaction.UserID).Username }}
    {{ dbSet .Reaction.UserID $dbKey $data }}
  {{else}}
    {{ dbDel .Reaction.UserID $dbKey }}
  {{end}}

  {{ scheduleUniqueCC $const.cc.update nil 1 11 (sdict ) }}
{{end}}
```

## Aditional Notes:
