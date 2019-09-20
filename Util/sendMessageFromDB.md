```

{{ $members := "" }}
{{ $has := false }}
{{ range (dbTopEntries .ExecData.pattern 60 0) }}
  {{ $mention := (joinStr "" "<@" .UserID ">") }}
  {{ $members = (joinStr " " $members   $mention) }}
  {{ $has = true }}
{{ end }}

{{ if $has }}
  {{ sendMessageNoEscape nil (joinStr "" .ExecData.msg $members ) }}
{{ end }}


```
