```
{{ $dur := (toDuration (mult 5  .TimeMinute)) }}
{{ $time := ( currentTime.Add ( toDuration ( mult -5 .TimeHour ) ) ).Truncate $dur   }}
{{ $displayTime := $time.Format "15:04"}}
{{ $t := joinStr "˸" (toString (printf "%02X" $time.Hour))  (toString (printf "%02X" $time.Minute)) }}
{{ editChannelName nil ( joinStr "" "Time--" $t )  }}
```
