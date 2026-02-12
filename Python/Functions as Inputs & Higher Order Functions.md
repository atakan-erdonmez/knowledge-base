
When you are passing a function as a parameter, you don't put paranthesis. Paranthesys mean 'execute the function right now'

```python 
def function_a(something):
	# do this with something
def function_b():
	# do this
	
function_a(function_b)
```


# Higher Order Functions
In Python, you can use functions inside functions. You can also pass them as parameters.

This is called higher order functions. It is a hierarchy