# FindRaidPartners

## Trigger Type:

Command

## Trigger:

trig

## Response:

```
{{/*__SET__ __Const__*/}}
<<Insert const here! $d />>

{{/********/}}

{{ range (dbGetPattern .User.ID $d.userVotePrefix 5 0 )}}


{{ else }}

{{ end }}
```
