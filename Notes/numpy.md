## **Numpy**
Lib for matrix compute.
==math== ==fast== ==compute==

### np.ndarray
Datatype: n dimension array
- .flags: memory distruibute
- .shape: dimensions turple
- .strides: index stride for dimensions
- .ndim: num of dimensions
- .data: point to begin of data storage
- .size: num of elems
- .itemsize: bytes of elments
- .nbytes: bytes of total storage
- .base: return where data refer to, or if it is base, return None.
- .dtype: data type of elem
- .T : transform matrix
- .real : real of complex
- .imag : imagine of complex
- .flat : one dimension iterator
- .ctypes: 
- ==TODO==

### np.array()
- np.array()

### functions
- np.linspace(start, end, step)
- np.stack([array list], axis=dimension_id)
	- stack arrays in dimension_id axis. dimension id start from 0.
	- stacked arrays dimension. 0 1 2 -> x 0 1 2 / 0 x 1 2. 
	- for 2D matrix, considering its logic. take 0 x 1 for example, 0 : : means a marix of n-st row of matrx. 0 x : means cloumn n-st row and n-st elemens.
	- usually, dimension_id = 0/n+1. =0 means a list of all elements. =n+1 means at any position of elemens now is a list of "cells" at that position of all elements.

### tips


