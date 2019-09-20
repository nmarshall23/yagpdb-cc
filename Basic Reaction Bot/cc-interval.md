# Command Name

## Trigger Type:

Command

## Trigger:

trig

## Response:

```
{{ $const := (sdict
    "dbPrefix" "test"
    "actionMsgKey" "test--actionMsgId"
    "channel" "test-channel"
    "emoji" (cslice "" "" "")
    "userValueDbPrefix" "test--user|"
    "userPattern" "test--user|%"
    "keys" (sdict
      "ex1" "test--kEx1"
    )
    "cc" (sdict
      "update" 0
      "reset" 0
      "sendReminder" 0
    )
    "role" (sdict
      "org" 622604425076277249
    )
  )
}}

{{ $time := currentTime.Add ( toDuration ( mult -5 .TimeHour ) )  }}
{{ $CurrHour := $time.Hour }}
{{ $minsDelay :=  (add 60 (mult -1 currentTime.Minute)) }}

{{with $const}}
  {{ $data := sdict "msg" "It's time to gather and attack!" }}

  {{if eq $CurrHour 1 }}
    {{ execCC .cc.reset nil 0 (sdict ) }}
  {{else if eq $CurrHour 16 }}
    {{ $role := mentionRoleID .role.org }}
    {{ sendMessageNoEscape nil (joinStr " " "A reminder" $role "did you happen to see what level tonight's Boss is?") }}
  {{end}}

  {{range $k, $v := (sdict
      "T🕕" 17
      "T🕖" 18
      "T🕗" 19
      "T🕘" 20
    ) }}
    {{if eq $CurrHour $v }}
      {{ $data.Set "pattern" (joinStr "" "BossFight--reminder|" $k) }}
      {{ execCC .cc.sendReminder nil $minsDelay $data }}
    {{end}}
  {{end}}
{{end}}
```

### Notes

An Hour Interval is run some mins after the hour.

Delays Reminder to be on the hour.
