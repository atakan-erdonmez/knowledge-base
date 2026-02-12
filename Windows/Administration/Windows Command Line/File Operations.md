move, xcopy, robocopy : Move files. Robocopy is the most updated
robocopy /MIR :  Mirror the source and dest. Deletes in dest too.

more \[/S] : Read file, with \/S, compress blank space together, less blank line. Can be used with pipes.

rmdir /S : Force delete

openfiles: Only admin. Show openfiles system-wide, like lsof
type: cat bildigin. You can append files via `type file.txt >> anan.txt

fsutil : Multiple purpose program
	`fsutil file createNew for-sure.txt 222`

find : grep /i ->  case insensitive
& -> ; (linux)     && -> &&      || -> ||

/A -> is an attribute flag that can be used in dir and del.
```cmd-session
  attributes    R  Read-only files            S  System files
                H  Hidden files               A  Files ready for archiving
                I  Not content indexed Files  L  Reparse Points
                O  Offline files              -  Prefix meaning not
```
del /A:R *

copy & move