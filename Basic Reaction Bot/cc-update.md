# Update Boss

## Trigger Type:

Command

## Trigger:

trig

## Response:

````
{{/*__SET__ __Const__*/}}
<<Insert const here! $d />>

{{/********/}}

{{/*__Retrieve Values__*/}}

{{ $description := "A wild boss has invited themselves in our Base! Who could it be?" }}
{{ with $dbValue := dbGet (toInt64 0) $d.key.bossName }}
  {{ $description = $dbValue.Value }}
{{ end }}


{{/*__Retrieve User Reaction__*/}}

{{$LookingForCoop := sdict }}

{{ $dbEntries := sdict
  "T🕕" " "
  "T🕖" " "
  "T🕗" " "
  "T🕘" " "
}}
{{ range (dbTopEntries (joinStr "" $d.key.userVotePrefix "%") 60 0) }}
  {{ $pattern := (split .Key "|") }}
  {{ $key := (joinStr ", " (index $pattern 1)) }}
  {{ $v := $dbEntries.Get $key }}
  {{$dbEntries.Set $key (joinStr " " $v .Value) }}
{{ end }}

{{ range $k, $v := $dbEntries }}
  {{ $LookingForCoop.Set $k (joinStr "" "```" $v "```") }}
{{ end }}


{{ $fields := cslice
  (sdict "name" "🕕 Looking for Co-op at 18:00" "value" ($LookingForCoop.Get "T🕕") "inline" false)
  (sdict "name" "🕖 Looking for Co-op at 19:00" "value" ($LookingForCoop.Get "T🕖") "inline" false)
  (sdict "name" "🕗 Looking for Co-op at 20:00" "value" ($LookingForCoop.Get "T🕗") "inline" false)
  (sdict "name" "🕘 Looking for Co-op at 21:00" "value" ($LookingForCoop.Get "T🕘") "inline" false)
}}

{{/*__Create Embed Msg__*/}}

{{ $embed := cembed
  "title"  "Boss Invasion"
  "description" $description
  "color" 4645612
  "fields" $fields
  "footer" (sdict "text" "Voting will send you a reminder. \nThere is a 1 sec delay before a vote registers.")
}}

{{ $retId := dbGet (toInt64 0) $d.keys.voteMsgId }}
{{ editMessage nil $retId.Value $embed }}
````

## Additional Notes:
