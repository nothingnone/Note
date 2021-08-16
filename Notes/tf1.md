### Session
```python
tf.Session(target, graph, config)
# tf use "compute graph" to define tensor compute.
# while compute graph tensor flow defined, execute on target devices with session.
# target: tensor flow to compute on target compute engine. eg: cpu0, gpu0, distribute devices.
# graph: compute graph.
# config: config. eg: log, cpu compute config.
# session function: reset(), run(), partial_run()...
session.run(fetches, feed_dict, options, run_metadata)
# fetches: list of graph elements to fetch.
# feed_dict: feed variables of placeholder inputs.
# finish compute should invoke session.close() to free resources. Or use "with" to open session context.
```
```python
tf.tensor.eval(feed_dict, session)
# evaluate value of tensor with feed_dict in session.
# if session is none, use default session. tf.InteractiveSession() return default session.
# use sess.as_default() to set sess default *in this thread*. 
```
```python
tf.train.optmi
```


```python
tf.nn.conv2d(input, filter, strides, paddings, \
use_cudnn_on_gpu, data_format, dilations, name, filters)
# data_format:"NHWC"/"CHWN".N:batch num, H:height, W:width C:channel.
# input: 4-D tensor as data_format.
# filter: 4-D kernel. [filter_height, f_w, in_channels, out_c] 
# strides: [1, x, y, 1]. x, y for conv kernel multi step.
# padding: "SAME"/"VALID". same, make up input to conv with kernel with 0.
# use_cudnn_on_gpu: default--true
# dilations: An int list with length 1(all)/2(height,width)/4(1,x,y,1, as data_format order). k>1,skip k-1 cells between each filter element on that dimension.
# filters: alias filter.
# output:
output[b, i, j, out_c] = 
sum_{di, dj, in_c} 
input[b, (strides.h*i+di)*dilation.h, (strides.w*j+dj)*dilation.w, in_c]
*filter[di, dj, in_c, out_c]
```

```python

```