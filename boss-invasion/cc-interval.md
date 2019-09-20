# Command Name

## Trigger Type:

Command

## Trigger:

trig

## Response:

```
{{/*__SET__ __Const__*/}}
{{/* Insert const here! */}}

{{ $time := currentTime.Add ( toDuration ( mult -5 .TimeHour ) )  }}
{{ $CurrHour := $time.Hour }}

{{with $const}}
  {{ $data := sdict "msg" "It's time to gather and attack!" }}

  {{if eq $CurrHour 1 }}
    {{ execCC .cc.reset nil 0 (sdict ) }}
  {{else if eq $CurrHour 16 }}
    {{ $role := mentionRoleID .role.org }}
    {{ sendMessageNoEscape nil (joinStr " " "A reminder" $role "did you happen to see what level tonight's Boss is?") }}
  {{end}}

  {{range $k, $v := (sdict
      "🕕" 17
      "🕖" 18
      "🕗" 19
      "🕘" 20
    ) }}
    {{if eq $CurrHour $v }}
      {{ $minsDelay :=  (add 60 (mult -1 currentTime.Minute)) }}
      {{ $data.Set "pattern" (joinStr "" .key.userVotePrefix "T" $k) }}
      {{ execCC .cc.sendReminder nil $minsDelay $data }}
    {{end}}
  {{end}}
{{end}}
```

### Notes

An Hour Interval is run some mins after the hour.

Delays Reminder to be on the hour.
