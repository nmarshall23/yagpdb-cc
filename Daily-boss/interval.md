```
{{ $sendMsgCC := 24 }}
{{ $viceBossScout := 622604425076277249 }}
{{ $resetBossCC := 5 }}
{{ $time := currentTime.Add ( toDuration ( mult -5 .TimeHour ) )  }}
{{ $CurrHour := $time.Hour }}

{{if eq $CurrHour 1 }}
  {{ execCC $resetBossCC nil 0 (sdict ) }}
{{else if eq $CurrHour 16 }}
  {{ $role := mentionRoleID $viceBossScout }}
  {{ sendMessageNoEscape nil (joinStr "" "A reminder " $role " did you happen to see what level tonight's Boss is?") }}
{{else if eq $CurrHour 18 }}
 {{ execCC $sendMsgCC nil 0 (sdict "msg" "It's time to gather and attack!" "pattern" "BossFight--reminder|T🕕" ) }}
{{else if eq $CurrHour 19 }}
  {{ execCC $sendMsgCC nil 0 (sdict "msg" "It's time to gather and attack!" "pattern" "BossFight--reminder|T🕖" ) }}
{{else if eq $CurrHour 20 }}
  {{ execCC $sendMsgCC nil 0 (sdict "msg" "It's time to gather and attack!" "pattern" "BossFight--reminder|T🕗" ) }}
{{else if eq $CurrHour 21 }}
  {{ execCC $sendMsgCC nil 0 (sdict "msg" "It's time to gather and attack!" "pattern" "BossFight--reminder|T🕘" ) }}
{{end}}

```
