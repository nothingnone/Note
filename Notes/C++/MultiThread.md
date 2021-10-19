# 

# practice
- dead lock case
	- implict dead lock loop logic. 
		- notice logical lock. lock in code is just a method to implement a lock.
		- eg: B hold mutex and free. A hold mutex and get B result then free. However, if A hold mutex first, won't get B result, keep holding. And B will block.
	- thread crash but not free lock.
- reinvoke function. 
	- during function, break at any time, then run any other code, then continue. No difference.
	- function is individual, thread safe.
- 