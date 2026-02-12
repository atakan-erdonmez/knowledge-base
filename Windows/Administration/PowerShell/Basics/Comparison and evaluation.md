### The Evaluation of Values

`Where` and many other cmdlets can `evaluate` objects and data based on the values those objects and their properties contain. The output above is an excellent example of this utilizing the `-like` Comparison operator. It will look for anything that matches the values expressed and can include wildcards such as `*`. Below is a quick list (not all-encompassing) of other useful expressions we can utilize:

#### Comparison Operators

|**Expression**|**Description**|
|---|---|
|`Like`|Like utilizes wildcard expressions to perform matching. For example, `'*Defender*'` would match anything with the word Defender somewhere in the value.|
|`Contains`|Contains will get the object if any item in the property value matches exactly as specified.|
|`Equal` to|Specifies an exact match (case sensitive) to the property value supplied.|
|`Match`|Is a regular expression match to the value supplied.|
|`Not`|specifies a match if the property is `blank` or does not exist. It will also match `$False`.|



[Comparison Operators](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_comparison_operators?view=powershell-7.2)



