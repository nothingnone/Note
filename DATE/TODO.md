- Kplanner 电梯地图更新static_layer代码开发
[] kplanner增加sub(/elevator_map) 和 clearElevGateCB()方法
[] clearElevGateCB()接受地图,将值为76的点map_layer清除,并且重新计算static_layer
[] 用normal_target测试,并且观察costmap和plan.