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
    {{ $minsDelay :=  (add 60 (mult -1 currentTime.Minute)) }}
    {{ $HoursDelay :=  (add 23 (mult -1 currentTime.Hour)) }}

    {{ $delay := (mult 60 $minsDelay (mult 60 $HoursDelay)) }}

    {{ $data := (userArg  .Reaction.UserID).Username }}
    {{ dbSetExpire .Reaction.UserID $dbkey $data $delay }}}
  {{else}}
    {{ dbDel .Reaction.UserID $dbkey }}
  {{end}}

  {{ scheduleUniqueCC $d.cc.update nil 1 0 (sdict ) }}
{{end}}
```

## Aditional Notes:
