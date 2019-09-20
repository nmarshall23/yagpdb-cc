```
{{ $myUserId := (toInt64 509925858270642206) }}
{{ $dbkey := "BossFight--voteMsgId" }}
{{ $channel := 621019962626015242 }}

{{ range (dbTopEntries "BossFight--reminder|%" 60 0) }}
  {{ dbDel .UserID .Key }}
{{ end }}

{{ dbDel $myUserId "Name_BossFight" }}
{{ $oldretId := dbGet $myUserId  $dbkey }}
{{ if $oldretId }}
   {{ deleteMessage $channel $oldretId.Value 1 }}
{{ end }}

{{$embed := cembed
"title" "__Boss Invasion__"
}}

{{ $retId := sendMessageRetID $channel $embed }}

{{ addMessageReactions $channel $retId "🕕" "🕖" "🕗" "🕘" }}

{{ dbSet $myUserId $dbkey (toString $retId) }}

{{ if .Message }}
{{ deleteTrigger 5 }}
{{ end }}
{{ execCC 15 $channel 2 (sdict ) }}

```
