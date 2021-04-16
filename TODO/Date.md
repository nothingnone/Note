### 4-6
窄电梯场景进入
进入电梯模式 -> 全局规划中清除障碍物 -> 局部规划中,保留电梯门处的障碍物 -> 调整局部规划参数,使其根据激光扫描的结果规划前行,允许偏离全局路径规划一定范围
代码实现
在local_cost_map中再加两个func层，在local中逐层修改。目前要调研的就是local_planner中costmap的添加,并尝试修改.问题来了,如何测试代码逻辑,可以尝试编写一个map_service进行测试.

### 4-15
窄电梯口通过策略修改
x. 可视化map,获取电梯口坐标。
x. 可视化kplan。
x. 实现costmap的可视化。
4. kplanner中实现clearElevGateCB()函数，清除电梯口区域。
5. move_base中，由于elev target导致coredump，因此采用normal target测试。考虑到更换地图的可能，初步采用在设值goal时就清一次。后续可在kplanner中添加标志位，只有当地图更新时才清除。
x. 修改电梯地图, 76
7. 修改机器型号配置
8. 阅读kplanner中的地图更新流程。

### 4-16
可视化
[] kplanner静态层与合成层的可视化.在kplanner中添加static_costmap_pub_, combine_costmap_pub. 在makeplan加锁前将这两个消息pub出去.
