```
{{ $time := ( currentTime.Add ( toDuration ( mult -5 .TimeHour ) ) ).Truncate $dur   }}
{{ $displayTime := $time.Format "15:04"}}

{{ editChannelName nil ( joinStr "" "Time-" $displayTime )  }}
```
