```
{{$args := parseArgs 1 "-setBossName <Text to replace description>"
    (carg "string" "boss-name")
}}

{{/*__SET__ __Const__*/}}
<<Insert const here! $d />>


{{ $name := $args.Get 0}}
{{ dbSet (toInt64 0) $d.keys.bossName $name }}

{{ execCC $d.cc.update $d.channel 1 (sdict ) }}
  {{ deleteTrigger 3 }}
{{end}}
```
