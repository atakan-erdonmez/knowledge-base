# Input function
This functions will  wait a response from the user. It will give the prompt 
```python
input("What is your name?")
```

The input() will change that code with the response it gets from the user

# Variables
```
my_var = "blabla"
```


## f-string
In order to use multiple datatypes in same print, you can use f-strings.

```python
print(f"ismim {string1}, yasim {integer1}, erkegim{boolean1})
```


# Data Types
## Strings
- When you want to get a specific character in a string, use brackets
- This is called *subscripting*
```python
print("Hello"[0])
# Will print H
```

- You can also start from the back, using *negatives*
- `print("hello"[-1])` -> will give "o"

## Integer
To create a number as an integer, you just have to type the number
- You can use *underscore* to replicate commas in large numbers, just for easier understanding
```python
print(123_456_789)
# Will print 123456789
```

### Math Equations
```python
print(12 + 3)
print(12 - 3)
print(12 * 4)
print(12 / 4)
print(3**3) # Expontent, which is 3^3)
print(10%3) # modulo, presents remaining, print 1
```

Note: When you divide a number with this, you will always get a float result. To get a integer result:
```python
print(12 // 4)
# This will print without float
```

> This type of division works by dividing first, then getting rid of float. So if it is not a clean division, it will give wrong error
## Float
A number with decimal

`var = 123.45`
## Boolean
It is just True or False