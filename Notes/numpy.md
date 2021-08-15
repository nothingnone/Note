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

### function
- np.stack([array list], axis=dimension_id)
	- stack arrays in dimension_id axis. dimension id start from 0.
	- stacked arrays dimension. 0 1 2 -> x 0 1 2 / 0 x 1 2. 