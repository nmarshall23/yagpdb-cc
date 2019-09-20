# Update Boss

## Trigger Type:

Command

## Trigger:

trig

## Response:

````
{{/*__SET__ __Const__*/}}
{{/* Insert const here! */}}

{{/*__Retrieve Values__*/}}
{{ $description := "A wild boss has invited themselves in our Base! Who could it be?" }}
{{with $const }}
  {{ with $dbValue := dbGet (toInt64 0) .key.bossName }}
    {{ $description = $dbValue.Value }}
  {{ end }}
{{ end }}


{{/*__Retrieve User Reaction__*/}}

{{$LookingForCoop := sdict }}

{{with $const }}
  {{ $dbEntries := sdict
    "T🕕" " "
    "T🕖" " "
    "T🕗" " "
    "T🕘" " "
  }}
  {{ range (dbTopEntries (joinStr "" .key.userVotePrefix "%") 60 0) }}
    {{ $pattern := (split .Key "|") }}
    {{ $n := (joinStr ", " (index $pattern 1)) }}
    {{ $v := $dbEntries.Get $n }}
    {{$dbEntries.Set $n (joinStr " " $v .Value) }}
  {{ end }}

  {{$defaultKeys := cslice "T🕕" "T🕖"  "T🕗" "T🕘" }}
  {{ range $k, $v := $defaultKeys }}
    {{ $group := ($dbEntries.Get $v) }}
    {{ $LookingForCoop.Set $v (joinStr "" "```" $group "```") }}
  {{ end }}
{{end}}


{{ $fields := cslice
  (sdict "name" "🕕 Looking for Co-op at 18:00" "value" ($LookingForCoop.Get "T🕕") "inline" false)
  (sdict "name" "🕖 Looking for Co-op at 19:00" "value" ($LookingForCoop.Get "T🕖") "inline" false)
  (sdict "name" "🕗 Looking for Co-op at 20:00" "value" ($LookingForCoop.Get "T🕗") "inline" false)
  (sdict "name" "🕘 Looking for Co-op at 21:00" "value" ($LookingForCoop.Get "T🕘") "inline" false)
}}

{{/*__Create Embed Msg__*/}}

{{with $const }}
  {{ $embed := cembed
  "title"  "Boss Invasion"
  "description" $description
  "color" 4645612
  "fields" $fields
  "footer" (sdict "text" "Voting will send you a reminder. \nThere is a 1 sec delay before a vote registers.")
  }}

  {{ $retId := dbGet (toInt64 0) .key.voteMsgId }}
  {{ editMessage nil $retId.Value $embed }}
{{end}}
````

## Additional Notes:
