**Procedural Programming:** Regular programming with functions and stuff

- Methods: Something an object *does*
- Attributes: Something an object *has*



```python
car = CarBlueprint()
# car -> object, CarBlueprint() -> class
```

# Create Class & Object

```python
class WebUser:
	pass
user1 = WebUser()
```

# Create Object & Add Attribute
```python
user1 = WebUser()
user1.id = '001'
user1.username = 'atakan'

print(user1.username) # will print atakan
```

## Initialize / Construct
When creating an object from a class, you can create attributes manually like above. However, it is hard and error-prone. To simplify, you use **constructs** or **initialize** an object.

In python, you do this using \_\_init\_\_. 

```python
class Car:
	def __init__(self):
	# initialize attributes
```

Every time an object is created, init function will be called.
- "self" keyword is used to assign attributes to the object being created.

```python
class User:
    def __init__(self,name='default_name'):
        self.username = name
        self.followers = 0 ## You can give attributes without any passing
user_1 = User('atakan')
user_2 = User('ela')
```

To have a placeholder in a parameter, you can use `__init__(self, name='placeholder')`.

# Add Methods
```python
class Car:
	def enter_race_mode(self):
		self.seats = 2
```

You generally need to give the "self" as the first parameter to change anything about the object

The 'init' method runs first when you create an object. Then, you can change a value assigned by 'init' by using any method