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

{{ $description := "Raid Partner Signup" }}



{{/*__Retrieve User Reaction__*/}}

{{$LookingForCoop := sdict }}

{{ $dbEntries := sdict
  "UmbralJade" ""
  "GrueJade" ""
  "GlowingJade" ""
}}
{{ range (dbTopEntries (joinStr "" $d.keys.userVotePrefix "%") 60 0) }}
  {{ $pattern := (split .Key "|") }}
  {{ $key := index $pattern 1 }}
  {{ $v := $dbEntries.Get $key }}
  {{ $dbEntries.Set $key (joinStr ", " $v .Value) }}
{{ end }}

{{ range $k, $v := $dbEntries }}
  {{ if $v }}
    {{ $LookingForCoop.Set $k (joinStr "" "```" $v "```") }}
  {{ else }}
    {{ $LookingForCoop.Set $k (joinStr "" "```   ```") }}
  {{ end }}
{{ end }}

{{ $fields := cslice
  (sdict "name" "<:UmbralJade:622628108142379028> Seeking Black Jade" "value" ($LookingForCoop.Get "UmbralJade") "inline" false)
  (sdict "name" "<:GrueJade:622628074969759754> Seeking Blue Jade" "value" ($LookingForCoop.Get "GrueJade") "inline" false)
  (sdict "name" "<:GlowingJade:622628038869254144> Seeking Orange Jade" "value" ($LookingForCoop.Get "GlowingJade") "inline" false)
}}

{{/*__Create Embed Msg__*/}}

{{ $embed := cembed
  "title"  "Raid Partner Signup"
  "description" "Select the Item you are looking for. Votes expire in 24 Hours."
  "color" 4645612
  "fields" $fields
  "footer" (sdict "text" "\nThere is a 1 sec delay before a vote registers.")
}}

{{ $retId := dbGet (toInt64 0) $d.keys.voteMsgId }}
{{ editMessage nil $retId.Value $embed }}
````

## Additional Notes:
