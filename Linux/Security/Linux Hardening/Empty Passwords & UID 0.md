# Empty Passwords
There should be no user account with empty password. Check empty passwords:
- `awk -F:'($2 == "!!") {print}' /etc/shadow`


Lock all empty password accounts:
`passwd -l accountName`
[[Linux/User Administration/General Commands|Passwd]]

# UID 0
No user except root should have UID 0
`awk -F: '($3 == "0") {print}' /etc/passwd`