| Character | Name(s)                | Uses                                                      |
| --------- | ---------------------- | --------------------------------------------------------- |
| `*`       | star, asterisk         | Regular expression, glob character                        |
| `.`       | dot                    | Current directory, file/hostname delimiter                |
| `!`       | bang                   | Negation, command history                                 |
| `\|`      | pipe                   | Command pipes                                             |
| `/`       | (forward) slash        | Directory delimiter, search command                       |
| `\`       | backslash              | Literals, macros (never directories)                      |
| `$`       | dollar                 | Variables, end of line                                    |
| `'`       | tick, (single) quote   | Literal strings                                           |
| `` ` ``   | backtick, backquote    | Command substitution                                      |
| `"`       | double quote           | Semi-literal strings                                      |
| `^`       | caret                  | Negation, beginning of line                               |
| `~`       | tilde, squiggle        | Negation, directory shortcut                              |
| `#`       | hash, sharp, pound     | Comments, preprocessor, substitutions                     |
| `[` `]`   | square brackets        | Ranges                                                    |
| `{` `}`   | braces, curly brackets | Statement blocks, ranges                                  |
| `_`       | underscore, under      | Substitute for space, avoids autocomplete or space issues |
