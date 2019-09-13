# UpdateBossEmbed

## Trigger Type:
Command

## Trigger:
UpdateBossEmbed

## Response:
```
{{ $myUserId := (toInt64 509925858270642206) }}
{{ $dbkey := "BossFight--voteMsgId" }}

{{ $retId := dbGet $myUserId  $dbkey }}

{{ $bossName := "A wild boss has invited themselves in our Base! Who could it be?" }}
{{ if (dbGet $myUserId "Name_BossFight") }}
 {{ $bossName := .Value }}
{{ end }}


{{$LookingForCoop := (sdict "Solo" " ** " )}}

{{ range (dbTopEntries "BossFight--reminder|%" 60 0) }}
   {{ $pattern := (split .Key "|") }}
   {{ $n := (joinStr ", " (index $pattern 1)) }}
   {{ $v := $LookingForCoop.Get $n }}
   {{$LookingForCoop.Set $n (joinStr " " $v .Value) }} 
{{ end }}

{{$defaultKeys := cslice "T🕕" "T🕖"  "T🕗" "T🕘" }}
{{ range $k, $v := $defaultKeys }}
 {{ $group := ($LookingForCoop.Get $v) }}

 {{ if not $group}}
    {{ $group := "  " }}
 {{ end }}
 {{ $LookingForCoop.Set $v (joinStr " " "```" $group "```") }}
{{ end }}


{{$embed := cembed 
"title"  "Boss Invasion"
"description" $bossName
"color" 4645612 
"fields" (cslice 
    (sdict "name" "🕕 Looking for Co-op at 20:00" "value" ($LookingForCoop.Get "T🕕") "inline" false) 
    (sdict "name" "🕖 Looking for Co-op at 21:00" "value" ($LookingForCoop.Get "T🕖") "inline" false)
    (sdict "name" "🕗 Looking for Co-op at 22:00" "value" ($LookingForCoop.Get "T🕗") "inline" false)
    (sdict "name" "🕘 Looking for Co-op at 23:00" "value" ($LookingForCoop.Get "T🕘") "inline" false)
)
"footer" (sdict "text" "Voting will send you a reminder. \nThere is a 1 sec delay before a vote registers.")
}}


{{ editMessage nil $retId.Value $embed }}
```

## Aditional Notes:
