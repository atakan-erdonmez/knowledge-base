# Generic & Data Types
## str()
Turns a data type into a string
## int()
Turns a data into a integer
**NOTE**: If converted from float, it will get rid of float completely, instead of rounding it. To do that, use *[[Built-in Functions#round()|round()]]*
## float()
Turns to float
## bool()
Turns to boolean
## len()
Calculate the length of a string
`print(len(my_name))`
## type()
Show the type of a variable
`type(var1)`
## print(''')
When you want to print multiple lines, you can use 3 single quote
```
print('''
oha
adama
bak
''')
```
# Number Manipulation
## round()
Round a float into a integer

```python
round(1.5)
# will print 2
```
`
- Round function can also round to a floating number via specifying digit
```python
round(2.8543,2)
# print 2.85
round(1.2341,3)
# print 1.234
```

## abs()
Return the absolute value of an integer
## Assignment Operator
You can use these instead of doing repeating operations.
```python
score += 1
score -= 1 
score *= 2
score /= 3
```

# Text Manipulation
## .lower()
Lowercase the string
`input('blabla').lower()`

## .strip()
Strip whitespaces

## .title()
Capitalize every letter of every word
# List Manipulation
## append()
To add an item to the end of the list, you use this function.

```python
tr_sehirler.append('denizli')
```

## insert()
Insert an item to a specified location
```python
tr_sehirler.insert(0,'zonguldak') # insert as the first of the list
tr_sehirler.insert(1,'adiyaman') # insert as the second of the list
```

## extend()
Add another list to the existing list
```python
tr_sehirler.extend(['bursa', 'burdur', 'tokat'])
```

## sum()
Sum of all the numbers in a list

## ![[random#random.choice(list)]]
## list()
Turns a string into a list by individual characters
```python
word = pencil
my_list = list(word)
# ['p','e',....]
```

## join()
It is used to join stuff. It can also be used to convert strings into text
```python
xs = ['1', '2', '3']
s = ''.join(xs)
```

## count()
Count how many times that item appears in the a list
```
points = [1,1,2,2,3,3,3,3]
x = points.count(3)
# x is 4
```

## index()
Give the position of an item in a list

![[Built-in Functions#max()]]

# Dictionary Manipulation

## items()
Used to iterate in a dictionary through both Key and Value at the same time
```python
for name, score in student_scores.items(): 
	grade = converter(score) 
	student_grades[name] = grade
```

## max()
Find the biggest number in a list or a dictionary
```python
# List
a = (1, 5, 3, 9)
x = max(a)

# Dictionary
scores = {
    "Alice": 50,
    "Zack": 10,
    "Harry" : 88
}

x = max(scores, key=scores.get)
```

This will basically iterate through every "key", and ".get" function is similar to using "\[]". So you basically say "Use scores dictionary, and key values are scores\[]"

| **Code**                      | **Returns**          | **Based On** |
| ----------------------------- | -------------------- | ------------ |
| `max(scores.values())`        | **88** (Number)      | Math         |
| `max(scores)`                 | **"Zack"** (String)  | Alphabet     |
| `max(scores, key=scores.get)` | **"Harry"** (String) | Math         |

## .get()
It can be used to select items in a dictionary like `my_dict["Harry"]`, but won't break the code if that item is non existent, it will return 'None'