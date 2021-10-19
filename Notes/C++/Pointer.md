# principle
- attribute
	- **type**, eg: int* .
	- **address**.
	- **value**, is value address.
- operation
	- *( p ) , get the **type** object at address **value**.
	- p = &( ) or address , assign address **value** to p. must same type or cast to same.
	- p-> same as *( p ). ,p must be a class.
	- 

# practice
- construction may fail, check if pointer is nullptr.



# Smart pointer
- circular reference
	- it's normal that two level class both have pointer of another.if use smart pointer to manage their lifetime, this cause circular reference, they will never be recycled.
	- use weak_ptr, this will not increase refer count.
	- this also happens in python. 
