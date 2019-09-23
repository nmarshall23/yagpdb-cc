```
{{ $dur := (toDuration (mult 5  .TimeMinute)) }}
{{ $time := ( currentTime.Add ( toDuration ( mult -5 .TimeHour ) ) ).Truncate $dur   }}
{{ $displayTime := $time.Format "15:04"}}
{{ $t := joinStr "˸" (toString $time.Hour)  (toString $time.Minute) }}
{{ editChannelName nil ( joinStr "" "Time--" $t )  }}
```
