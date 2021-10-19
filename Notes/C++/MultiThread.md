# 

# practice
- dead lock case
	- implict dead lock loop logic. 
		- eg: B hold mutex and free. A get B return and hold mutex thne free. However, if A hold mutex 
		- notice logically hold lock.
	- thread crash but not free lock.
- while waiting, must get. while holding, must release.
- 