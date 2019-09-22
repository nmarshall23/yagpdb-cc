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

{{ $role := mentionRoleID $d.role.org }}
{{ $local := sdict
  "userMessage" "It's time to gather and attack!"
  "userKeysHour" (sdict
    "T🕕" 17
    "T🕖" 18
    "T🕗" 19
    "T🕘" 20
  )
  "organizerReminder" (joinStr " " "A reminder" $role "did you happen to see what level tonight's Boss is?")
}}

{{/********/}}

{{ $time := currentTime.Add ( toDuration ( mult -5 .TimeHour ) )  }}
{{ $CurrHour := $time.Hour }}


{{if eq $CurrHour 1 }}
  {{ execCC $d.cc.reset nil 0 (sdict ) }}
{{else if eq $CurrHour 16 }}
  {{ sendMessageNoEscape nil $local.organizerReminder}}
{{end}}

{{range $k, $v := $local.userKeysHour }}
  {{if eq $CurrHour $v }}
    {{ $data := sdict
      "msg" $local.userMessage
      "pattern" (joinStr "" $d.keys.userVotePrefix $k)
    }}
    {{ $minsDelay :=  (add 60 (mult -1 currentTime.Minute)) }}
    {{ $delay := (mult 60 $minsDelay) }}

    {{ execCC $d.cc.sendReminder nil $delay $data }}}
  {{end}}
{{end}}
```

### Notes

An Hour Interval is run some mins after the hour.

Delays Reminder to be on the hour.
