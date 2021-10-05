# data

# model

# train
## maximum likehood requires independent identically distributed
Key: batch or neighbour steps date must provide the right gradient.
Extreme situation: considering a net with one output node, queue train data by increase order and train one cycle. The output will increase in training, just like a filter, and the final value will depend on the gradient decent step, but not the average. If we train cycles, and if step is very small, finally we will get the average. Or if step is big, the output will oscillate.
At present, dont't know what will cause above problem. However, remember that key is ***batch or neighbour steps date must provide the right gradient***.