```
{{ $myUserId := (toInt64 509925858270642206) }}
{{ $channel := 621019962626015242 }}


{{$args := parseArgs 1 "-dailyBossSetName <Text to replace description>"
    (carg "string" "boss-name")
}}

{{$name := $args.Get 0}}
{{ dbSet $myUserId "Name_BossFight" $name }}

{{ execCC 15 $channel 1 (sdict ) }}
{{ deleteTrigger 3 }}

```
