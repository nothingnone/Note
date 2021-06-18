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
- teb, judge elevmode, increase xy_goal_tolerance,add.
- yaw_goal_tolerance to pi/2 to ignore pose orientation.attention!
- 当处于旋转过程中，需要精确规划，降低tolerance。如何编写代码？useElevMode(false)
- 在旋转过程中，同样需要计算超时,一旦超时,按失败处理.
- 修改goalReachedCheck(),电梯目标点需检查方向是否一致
- 当超时/goal丢弃时,需要resetflag.难以实现,且易错.当接收到新的goal,进行一次检查,若是电梯goal或者其他则resetflag.添加resetElevProcessFlag(), 并在handlenewgoal()时invoke.
- once inside elev. if inside and flag false, publish and setflag.
- once 出电梯. if out and flag false, publish and setflag.
- 0: once inside; 1:Reach Around!(get goal accurate); 2: Not reach!(get goal inaccurate); 3: once outside elev; 4:spin not finished!;5:spin finished.
- 问题!在电梯内放弃了任务,或有其他状况, 如何保证正确.
- 宽松goal参数会导致较大的刹车加速度，此时速度并非0；
- teb计算goalreached()，在computeVelocityCommands()中计算速度位置是否满足goal_tolerance.若是,则在goalreached()将标志位置1.而每次调用computeVelocityCommands()都会进行检查.目前的问题是spinTowardGoal()是否会导致goalReachedCheck()失效.
- teb增大tolerance带来的问题是，即使我能够走到目标点，也不会准确的走到目标点。而我们希望达到的结果是，在尽可能走到目标点的前提下终止.
- spinAround 超时设置在spin指令处. 

- 5-20
- [] 整理他们需要的接口.
	- 电机解锁状态与解锁原因
	- database是如何存储、拿取数据的。server
	- 
- [] 机器人上的性能分析.
- [] 目前而言，比较重要的就是低调做事，能够对事情有正确的判断，从大局出发如何合理的处理，是处理还是上报，必须要准确。综合而言，掌握形势，审时度势，张弛有度，灵活应对。
- [] 整理一下荧光涂料的问题。

- 5-21
- [] 配置好机器人的perf环境。重新安装指定包。
- 关于perf的问题。不同内核版本的perf源码相对稳定，但perf编译所需求的包可能14.04可能已经不兼容。

- 6-15
- [] 进电梯流程上报的旋转问题,大概率仍然是部署的电梯点问题，也可能是没有安装最新的teb的问题导致的混乱bug?? Big Question!
- [] 关于重定位信号的触发。目前的需求是客房前，电梯前触发重定位信号。目前采取的策略是到达目标点时触发重定位信号。阅读service的写法,并完成程序修改.
- [] 首先改写信号发送代码。当机器人旋转到指定角度后发5.旋转超时则发送4.

- 6-16
- [] 复制机器上的头文件到本地,并编写到达目标点后触发重定位服务的代码.
- [] 在机器上编译通过代码.
- [] 转圈问题.
- [] 测试思岚雷达

- 6-17
- [x] 关于传感器数据丢失后触发定位微调的问题。
- [] 关于联调测试的问题.时间定在下周。
- [] 关于原地转圈的问题的分析.
- valgrind
- 关于性能分析的问题.
- 关于长期项目,化整为零,化长为短,香肠战术.
- 凡是预则立,不预则废.

**关于转圈/振荡问题**
对于原地快速转圈,采取的策略为计算上一路径与当前路径在当前costmap中的总代价.计算两路径间的距离.综合距离,代价决定是否选择新的路径.
- 代价:在同一膨胀代价地图下.若两路径差距较大但cost值差距不大,则不必切换.若两路径cost值差距较大,应当以前一值为准.当上一路径与当前路径的长度不一致.针对该问题,可以削减,但削减的逻辑较为复杂.也可以不削减,因为短时间内的长度变化不大.需要归一化,因为希望有统一的标准.如何归一化?平均值?几何均值? 目前可以采取平均值的方式进行尝试.
- 距离.判断两个路径间的距离.目前采取的方式是计算曼哈顿距离,曼哈顿距离必须加权,近大远小,并进行归一化.甚至只截取前段计算.
- 选择.由于路径具有逻辑性质,难以通过简单有效的方式进行加权.因此只能在二者进行二选一.
对于长距离的振荡,需要采取障碍物长短时记忆策略.关于该策略的具体实现,以后再进行探讨.

- 6-18
- 阅读kplanner代码,尝试修改.
- 编译与定位的接口.
- 不要再构造函数里shared_from_this()传递本类的指针。
- ICRA会议,前沿期刊必须要研究一下.
- 产业报告研究.
- https://zhuanlan.zhihu.com/p/104051892查看
- 关于时间规划的问题

- 查bug.
elev out door res:2 ,open/close: 160/74
newgoalAvailable 新旧目标点相同
receive stop signal

- teb 性能优化