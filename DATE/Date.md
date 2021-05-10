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
可视
- [x] kplanner静态层与合成层的可视化.在kplanner中添加static_costmap_pub_, combine_costmap_pub. 在makeplan加锁前将这两个消息pub出去.
占用太大，fail。
- [x] 等待测试环境，等测试结果。
- [x] 整理代码
- [x] 形成文档。

### 4-17
仿真集成测试
- [ ] 整合SVG装置模型,确定第一版参数,并整合测试.
- [ ] 规范化参数.
- [ ] 微调参数.
- [ ] 最好能够完成仿真工作。

### 4-19
结项
- [x] 测试70~80cm的成功率:
测试方法:手画虚拟墙, 建地图, 建电梯地图, 76标注区域, 测试.
- [x] 输出结论, 总结并输出文档.
- [x] 复测, 查看call进梯点是否会触发crowdedplan.会触发,但无关.
- [ ] 大数据传输的可视化问题。比如采用外置内存
测试结论：
当出现有一侧激光墙壁不能探测到时，会出现斜角度约20度，减速进入电梯。
目标点的相对位置发生偏移时，kplanner规划的最短路径仍可优化。
前段最短有不稳定的搜索问题，贴边减速，而不是一个弧线。
70cm有减速斜进入的现象，概率不低，10cm，不安全。
当电梯门口有人候梯时，会给予一定的避障压力。
关于电梯内的不避障策略，可以采用超时措施。当超过一定时间，重规划。
由于是初测，不能与实际场景完全匹配。注意当要求提到这边时如何应对。
需要对

### 4-20
- [] 学习git团队协作
- [] 阅读梳理move_base
- 目前存在的问题是，以挤的方式，容易把机器人自己挤死。global_plan failed.
需要允许后退。
- 需要添加kplanner的数据记录。
- 目前这种通过调节参数，改变路径规划效果的方式。
- [ ] 

### 4-22
- [ ] 给运动状态上报做个强制滤除。

### 5-6
- [] 考虑采用原版还是采用新版进行性能测试。考虑原版，较为干净，后续的开发也可以在原版上。
- [] 调研teb算法的评价与细节。
- 性能优化方向：cost计算量，导数计算量。迭代次数。超图元素数量。策略上带来的计算量。

### 5-8
change:
- 头文件,源文件添加pub,sub
- 新建分支f-elev-signal，在其上开发.
- 接受信号后旋转，CB函数spinAroudToGoal()
- 开发spinAroundToGoal()函数,目前使用setSpinAroundAngle()方法,只需调用一次即可旋转到位。其原理和细节有待进一步确认。
- 添加receive_loc_signal_flag_, elev_loc_signal callback func. set flag.
- teb, judge elevmode, increase xy_goal_tolerance,add yaw_goal_tolerance to pi/2 to ignore pose orientation.attention!
- 当处于旋转过程中，需要精确规划，降低tolerance。如何编写代码？useElevMode(false)
- 在旋转过程中，同样需要计算超时,一旦超时,按失败处理.
- 修改goalReachedCheck(),电梯目标点需检查方向是否一致
- 当超时/goal丢弃时,需要resetflag.难以实现,且易错.当接收到新的goal,进行一次检查,若是电梯goal或者其他则resetflag.添加resetElevProcessFlag(), 并在handlenewgoal()时invoke.
- once inside elev. if inside and flag false, publish and setflag.
- once 出电梯. if out and flag false, publish and setflag.
- 0: once inside; 1:get goal accurate; 2: get goal inaccurate; 3: once outside elev.
- 问题!在电梯内放弃了任务,或有其他状况, 如何保证正确.
- 宽松goal参数会导致较大的刹车加速度，此时速度并非0；
- teb计算goalreached()，在computeVelocityCommands()中计算速度位置是否满足goal_tolerance.若是,则在goalreached()将标志位置1.而每次调用computeVelocityCommands()都会进行检查.目前的问题是spinTowardGoal()是否会导致goalReachedCheck()失效.

