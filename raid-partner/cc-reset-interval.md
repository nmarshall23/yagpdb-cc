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
{{ $hour := $time.Hour }}

{{if (or (eq $hour 1) (eq $hour 2 ))  }}
  {{ execCC $d.cc.reset nil 0 nil }}
{{end}}

```

### Notes

An Hour Interval is run some mins after the hour.

Delays Reminder to be on the hour.
