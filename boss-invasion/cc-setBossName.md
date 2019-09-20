```
{{$args := parseArgs 1 "-setBossName <Text to replace description>"
    (carg "string" "boss-name")
}}

{{/*__SET__ __Const__*/}}
{{/* Insert const here! */}}


{{with $const}}
  {{ $name := $args.Get 0}}
  {{ dbSet (toInt64 0) .key.bossName $name }}

  {{ execCC .cc.update .channel 1 (sdict ) }}
  {{ deleteTrigger 3 }}
{{end}}
```
