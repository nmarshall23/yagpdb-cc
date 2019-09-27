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
    {{ $delay := mult 3600 48 }}

    {{ $data := (getMember  .Reaction.UserID).Nick }}
    {{ if not $data }}
      {{ $data = (userArg  .Reaction.UserID).Username }}
    {{ end }}

    {{ giveRoleID .Reaction.UserID ($d.role.Get (joinStr "" "seeking" .Reaction.Emoji.Name)) }}
    {{ dbSetExpire .Reaction.UserID $dbkey $data $delay }}
  {{else}}
    {{ takeRoleID .Reaction.UserID ($d.role.Get (joinStr "" "seeking" .Reaction.Emoji.Name)) }}
    {{ dbDel .Reaction.UserID $dbkey }}
  {{end}}

  {{ scheduleUniqueCC $d.cc.update nil 1 0 (sdict ) }}
{{end}}
```

## Aditional Notes:
