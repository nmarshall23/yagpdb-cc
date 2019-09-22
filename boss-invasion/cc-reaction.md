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

    {{ $time := currentTime.Add ( toDuration ( mult -5 .TimeHour ) )  }}
    {{ $minsDelay :=  (add 60 (mult -1 $time.Minute)) }}
    {{ $HoursDelay :=  (add 23 (mult -1 $time.Hour)) }}

    {{ $delay := (add (mult 60 $minsDelay) (mult 3600 $HoursDelay)) }}

    {{ $data := (getMember  .Reaction.UserID).Nick }}
    {{ if not $data }}
      {{ $data = (userArg  .Reaction.UserID).Username }}
    {{ end }}

    {{ dbSetExpire .Reaction.UserID $dbkey $data (toInt64 $delay) }}
  {{else}}
    {{ dbDel .Reaction.UserID $dbkey }}
  {{end}}

  {{ scheduleUniqueCC $d.cc.update nil 1 0 (sdict ) }}
{{end}}
```

## Aditional Notes:
