# Command Name

## Trigger Type:

Command

## Trigger:

trig

## Response:

````
{{/*__SET__ __Const__*/}}
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
    )
  )
}}

{{/*__Retrieve Values__*/}}

{{ $description := "A wild boss has invited themselves in our Base! Who could it be?" }}
{{ $dbValue := dbGet (toInt64 0) $const.keys.ex1 }}
 {{ if $dbName}}
 {{ $description = $dbValue.Value }}
{{ end }}


{{/*__Retrieve User Reaction__*/}}

{{$dbMap := (sdict )}}

{{ range (dbTopEntries $const.userPattern 60 0) }}
   {{ $pattern := (split .Key "|") }}
   {{ $key := (joinStr "" (index $pattern 1)) }}
   {{ $v := $dbMap.Get $key }}
   {{$dbMap.Set $key (joinStr " " $v .Value) }}
{{ end }}

{{$defaultKeys := cslice
  "T🕕" "18:00"
  "T🕖" "19:00"
  "T🕗" "20:00"
  "T🕘" "21:00"
}}

{{ $entries := sdict }}
{{ range $k, $v := $defaultKeys }}
  {{ $group := ($dbMap.Get $v) }}

 {{ if not $group}}
    {{ $group := "  " }}
 {{ end }}
 {{ $LookingForCoop.Set $v (joinStr " " "```" $group "```") }}
 {{ $entries.Set }}
 {{ $

 }}
  (sdict "name" "🕕 Looking for Co-op at 18:00" "value" ($LookingForCoop.Get "T🕕") "inline" false)
{{ end }}

{{ $fields := cslice }}

{{/*__Create Embed Msg__*/}}

{{$embed := cembed
"title"  "Add Title"
"description" $description
"color" 4645612
"fields" (cslice
    (sdict "name" "🕕 Looking for Co-op at 18:00" "value" ($LookingForCoop.Get "T🕕") "inline" false)
)
"footer" (sdict "text" "Voting will send you a reminder. \nThere is a 1 sec delay before a vote registers.")
}}

{{ $retId := dbGet (toInt64 0) $const.actionMsgKey }}
{{ editMessage nil $retId.Value $embed }}

````

## Aditional Notes:
