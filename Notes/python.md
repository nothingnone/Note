### tips
- python '=' is alias.
- assign and copy problem.
- multi inherit problem

### Decorator
```python
# origin
def decorator(func, param):
	def wraps_func():
		return
	return wraps_func
decorated_func = decorator(origin_func)
decorated_func.__name__ 	# wraps_func
func = func


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
#

# use decorator class
class decorator(object):
	def __init__(self, param):
		super(decorator, self).__init__(param)
	def __call__(self, func, param):
		@wraps(func)	
		def wraps_func():
			return
		return wraps_func
@decorator(param)
def origin_func():
	return
# attention! use class as decorator, will invoke __call__() function.
# if you wanna init class, use this.
```
