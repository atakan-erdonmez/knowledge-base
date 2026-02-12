## Explanation of PowerShell Output (Objects Explained)

With PowerShell, not everything is generic text strings like in Bash or cmd. In PowerShell, everything is an `Object`. However, what is an object? Let us examine this concept further:

`What is an Object?` An `object` is an `individual` instance of a `class` within PowerShell. Let us use the example of a computer as our object. The total of everything (parts, time, design, software, etc.) makes a computer a computer.

`What is a Class?` A class is the `schema` or 'unique representation of a thing (object) and how the sum of its `properties` define it. The `blueprint` used to lay out how that computer should be assembled and what everything within it can be considered a Class.

`What are Properties?` Properties are simply the `data` associated with an object in PowerShell. For our example of a computer, the individual `parts` that we assemble to make the computer are its properties. Each part serves a purpose and has a unique use within the object.

`What are Methods?` Simply put, methods are all the functions our object has. Our computer allows us to process data, surf the internet, learn new skills, etc. All of these are the methods for our object.


## User perspective

```powershell-session
Get-LocalUser administrator | get-member
Get-LocalUser * | Select-Object -Property Name,PasswordLastSet

Show properties and methods of user(s)

Get-LocalUser * | Sort-Object -Property Name | Group-Object -property Enabled
```