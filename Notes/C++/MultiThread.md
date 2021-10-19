# 

# practice
- dead lock case
	- implict dead lock loop logic. 
		- eg: B hold mutex and free. A hold mutex and get B result then free. However, if A hold mutex first, won't get B result, keep holding. And B will block.
		- notice logically lock. ever
	- thread crash but not free lock.
- while waiting, must get. while holding, must release.
- 