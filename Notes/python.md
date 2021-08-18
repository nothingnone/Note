### tips
- python '=' is alias.
- assign and copy problem.
- multi inherit problem

### Super, Multi inherit
```python
class Child(parents):
	super(Child, self) 	# py2, return refer to parent.
	super() 		# py3, same as above.

class child(parent1, parent2):
	super.func()
# multi inherit, and diamond inherit
# from sub to parent, wide
```

### Decorator
```python
# origin
def decorator(func, param):
	def wraps_func():
		return
	return wraps_func
decorated_func = decorator(origin_func)
decorated_func.__name__ 	# wraps_func
func = decorator(func)		# decorated func


# use @ and functools.wraps
from functools import wraps
def decorator(func):
	@wraps(func)	#wraps wrap wraps_func with func param.
	def wraps_func():
		return
	return wraps_func
@decorator
def origin_func():
	return
origin_func.__name__ 	#origin_func
# now decorator don't change origin_func attributes.
# use func of @func to decorate.

# wanna a decorator with param
def decorator(param):
	def func_handle(func):
		@wraps(func)
		def wraps_func():
			return
		return wraps_func
	return func_handle

# use decorator class
class decorator(object):
	def __init__(self, param):
		super(decorator, self).__init__(param)
	def __call__(self, func):
		@wraps(func)	
		def wraps_func():
			return
		return wraps_func
@decorator(init)
# use init to init decorator, and return a decorator object, which can be call.
def origin_func():
	return
```
