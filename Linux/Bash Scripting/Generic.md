# IF statements

if \[ condition \]
then 
		code here
elif \[ condition \]
then
		code here
else
		code here
fi

# Arguments
$0 -> script
$1 - 9 -> arguments from 1 to 9

# Special Variables

Special variables use the [Internal Field Separator](https://bash.cyberciti.biz/guide/$IFS) (`IFS`) to identify when an argument ends and the next begins. Bash provides various special variables that assist while scripting. Some of these variables are:

|**IFS**|**Description**|
|---|---|
|`$#`|This variable holds the number of arguments passed to the script.|
|`$@`|This variable can be used to retrieve the list of command-line arguments.|
|`$n`|Each command-line argument can be selectively retrieved using its position. For example, the first argument is found at `$1`.|
|`$$`|The process ID of the currently executing process.|
|`$?`|The exit status of the script. This variable is useful to determine a command's success. The value 0 represents successful execution, while 1 is a result of a failure.|
<u>**Note**: When assigning variables, there must be no spaces between the names and values.</u>

# Arrays
```bash
domains=(www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com www2.inlanefreight.com)
```
```bash
domains_more=("www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com" www2.inlanefreight.com)
```

double and single quotes are used for strings with space.

```bash
echo ${domains[0]}  -> 
www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com www2.inlanefreight.com


echo ${domains_more[0]} -> 
www.inlanefreight.com ftp.inlanefreight.com vpn.inlanefreight.com 


echo ${domains_more[1]} -> 
www2.inlanefreight.com

```
