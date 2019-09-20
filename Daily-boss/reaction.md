# Reaction

## Trigger Type:
Reaction

## Response:
```
{{/* Setup */}}
{{ $updateBossCC := 15 }}
{{ $myUserId := (toInt64 509925858270642206) }}
{{ $dbkeyMsgId := "BossFight--voteMsgId" }}

{{/* Ignore Reactions from Bot */}}
{{ $AuthorId := .ReactionMessage.Author.ID }}
{{ if not (eq .Reaction.UserID $AuthorId) }}

	{{/* Ignore Reactions on other Messages */}}
	{{ $retId := dbGet $myUserId  $dbkeyMsgId }}
	{{ if eq .ReactionMessage.ID $redId.Value }}

		{{ $dbkey := (joinStr "" "BossFight--reminder|" "T" .Reaction.Emoji.Name) }}

		{{ if (.ReactionAdded) }}
		  {{ $name := (userArg  .Reaction.UserID).Username }}
		  {{ dbSetExpire .Reaction.UserID $dbkey $name  72000 }}
		{{else}}
		  {{ dbDel .Reaction.UserID $dbkey }}
		{{end}}

		{{ scheduleUniqueCC $updateBossCC nil 1 0 (sdict ) }}
	{{end}}
{{end}}
```

## Aditional Notes:


