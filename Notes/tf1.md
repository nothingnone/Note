```python
tf.nn.conv2d(input, filter, strides, paddings, \
use_cudnn_on_gpu, data_format, dilations, name, filters)
# data_format:"NHWC"/"CHWN".N:batch num, H:height, W:width C:channel.
# input: 4-D tensor as data_format.
# filter: 4-D kernel. [filter_height, f_w, in_channels, out_c] 
# strides: [1, x, y, 1]. x, y for conv kernel multi step.
# padding: "SAME"/"VALID"
# use_cudnn_on_gpu: default--true
# dilations: An int list with length 1/2/4. k>1,skip k-1 
```