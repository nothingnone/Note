### tips
- python '=' is alias.
- assign and copy problem.
- multi inherit problem

### Name, Object
```python
# name, object
a = 1
# py new a object--1, new a name--a, a point to 1.
a = 2
# py new a object--2, a point to 2.
b = a
# b point to a?
b = 10
a == 2
# or
a = 10
b == 2
# b not point to a.
a = []
b = a
a.append(1)
b == [1]
b.append(2)
a == [1,2]
# now b point to a?
# No!
a = a[:]
a is b # False
# so why?  
# In python, we call constant(int,float,str,tuple) immutable.
# list, dict, container and class is mutable.
# b = a , mean b point to object as a point to.
# for mutable, change 'a' point to object, but not change which one, will not change 'a' point to. So 'a' and 'b' point to same object. it seems that b is a.
# Good example:
a = 1
b = 1
a is b 	# True
a = []
b = []
a is b 	# False
a = []
id(a) 	# 000000..1
a.append(1)
id(a) 	# 000000..1
a = a[:]
id(a) 	# 000000..2 changed!
# Good Example.
a = [1,2,3]
b = [a[2],a[1],a[0]]
a is b 		# False
a[0] is b[0] 	# True
b[0] = -1 # b[0] # id changed.
a[0] is b[0] 	# False
class A():
	pass
a = [A(),A()]
b = [a[0],b[1]]
a is b # False
a[0] is b[0] 	# True
a[0].x = 1 	# a[0] id not changed.
b[0].x == 1
```

```python
# add module search path
import sys
sys.path.append(r"relative/path or /absolute/path")
```
```python
dir(obj)	# return summary of obj, attributes and methods.
help(obj)	# return manual of object, which is written by author.
```

### Super, Multi inherit
```python
class Child(parents):
	super(Child, self) 	# py2, return refer to parent.
	super() 		# py3, same as above.

class child(parent1, parent2):
	super.func()
# multi inherit, and diamond inherit. search method in principls as follows.
# from sub to parent, wide-first, in turn, only once.
```

### Decorator
```python
# origin
def decorator(func):
	def wraps_func(param):
		return
	return wraps_func
decorated_func = decorator(origin_func)
decorated_func.__name__ 	# = wraps_func
func = decorator(func)		# decorated func
func(param)

# use @ and functools.wraps
from functools import wraps
def decorator(func):
	@wraps(func)	#wraps wrap wraps_func with func param.
	def wraps_func(param):
		return
	return wraps_func
@decorator
def origin_func():
	return
origin_func.__name__ 	# = origin_func
origin_func(param)
# now decorator don't change origin_func attributes.
# use func of @func to decorate.

# wanna a decorator with param
def decorator(param_1):
	def func_handle(func):
		@wraps(func)
		def wraps_func(param):
			return
		return wraps_func
	return func_handle
@decorator(param_1)
origin_func(param)

# use decorator class
class decorator(object):
	def __init__(self, param_1):
		super(decorator, self).__init__(param_1)
	def __call__(self, func):
		@wraps(func)	
		def wraps_func(param):
			return
		return wraps_func
@decorator(param_1)
# use init to init decorator, and return a decorator object, which can be call.
def origin_func(param):
	return

# In Conclusion.
# In python, func is a object which is callable.
# it can be function or param, according to operator parsing. () operator has a high priority. 
# decorated_func(param) = param --> decorated_func = wraps_func(func) .__call__(param)
```
