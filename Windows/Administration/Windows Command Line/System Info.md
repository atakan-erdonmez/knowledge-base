systeminfo: Give info about hotfixes, network adapters, host name etc.
hostname,ver(version),ipconfig, arp /a
whoami: An extended tool for identification
	/priv: Show security privileges
	/groups: Show group info
		**Note:** If the current user is not a domain-joined account, the `NetBIOS` name will be provided instead. The current `hostname` will be used in most cases.
	/all : Show all (ne kadar komik ehuehue)
	

where -> find files in system
	/R: recursive & specify location if not in env variables
find -> find strings in files
	`C:\Users\student\Desktop> find "password" "C:\Users\student\not-passwords.txt`
	We can modify the way `find` searches using several switches. The `/V` modifier can change our search from a matching clause to a `Not` clause. So, for example, if we use `/V` with the search string password against a file, it will show us any line that does not have the specified string. We can also use the `/N` switch to display line numbers for us and the `/I` display to ignore case sensitivity. In the example below, we use all of the modifiers to show us any lines that do not match the string `IP Address` while asking it to display line numbers and ignore the case of the string.
	`C:\Users\student\Desktop> find /N /I /V "IP Address" example.txt`
	For quick searches, find is easy to use, but it could be more robust in how it can search. However, if we need something more specific, findstr is what we need. The findstr command is similar to find in that it searches through files but for patterns instead. It will look for anything matching a pattern, regex value, wildcards, and more. Think of it as find2.0. For those familiar with Linux, findstr is closer to grep.


comp -> compare two files
	`Comp` will check each byte within two files looking for differences and then displays where they start. By default, the differences are shown in a decimal format. We can use the `/A` modifier if we want to see the differences in ASCII format. The `/L` modifier can also provide us with the line numbers.

fc -> compare two files with more detailed and based on lines 
sort -> sort files
	/unique: show only unique lines
