
In order to use modules, you should import them at the start.
If you created your own module, you have to import it too.


- In order to use a variable from a module, you have to specify it with a dot.
```python
import my_module
print(my_module.mynumber)
```


Also, you can import specific functions from modules
```python
from my_module import mynumber, other_number

mynumber()
```


You can give aliases to specific modules
```python
import turtle as t
```