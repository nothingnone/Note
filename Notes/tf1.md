```python
tf.nn.conv2d(input, filter, strides, paddings, \
use_cudnn_on_gpu, data_format, dilations, name, filters)
# data_format:"NHWC"/"CHWN".N:batch num, H:height, W:width C:channel.
# input: 4-D tensor as data_format.
# filter: 4-D kernel. [filter_height, f_w, in_channels, out_c] 
# strides: [1, x, y, 1]. x, y for conv kernel multi step.
# padding: "SAME"/"VALID"
# use_cudnn_on_gpu: default--true
# dilations: An int list with length 1(all)/2(height,width)/4(1,x,y,1, as data_format order). k>1,skip k-1 cells between each filter element on that dimension.
# filters: alias filter.
# output:
output[b, i, j, out_c] = 
sum_{di, dj, in_c} 
input[b, (strides.h*i+di)*padding.h, (strides.w*j+dj)*padding.w, in_c]
*filter[di, dj, in_c, out_c]
```