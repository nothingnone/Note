### tips
- python '=' is alias.
- assign and copy problem.
- multi inherit problem

### decorator
```python
# origin
def decorator(func, param):
	def wraps_func():
		return
	return wraps_func
decorated_func = decorator(origin_func)
decorated_func.__name__ 	# wraps_func
origin_func()


# use @ and functools.wraps
from functools import wraps
def decorator(func, param):
	@wraps(func)	#wraps wrap wraps_func with func param.
	def wraps_func():
		return
	return wraps_func
@decorator(param)
def origin_func():
	return
origin_func.__name__ 	#origin_func
# now decorator don't change origin_func attributes.

# use decorator class
class decorator(object):
	def __init__(self, param):
		super(decorator, self).__init__(param)
	def __call__(self, func):
		@wraps(func)	
		def wraps_func():
			return
		return wraps_func

@
```
