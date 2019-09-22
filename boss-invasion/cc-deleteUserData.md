```
{{/*__SET__ __Const__*/}}
<<Insert const here! $d />>

{{/********/}}

{{ range (dbTopEntries (joinStr "" $d.keys.userVotePrefix "%") 60 0) }}
  {{ dbDel .UserID .Key }}
{{ end }}
```
