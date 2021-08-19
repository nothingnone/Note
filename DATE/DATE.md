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
目前有四个方向
(优先)降低构建超图点和边的数量
(优先)降低迭代次数(强制与情景)
雅克比矩阵计算
构建超图时点和边的遍历

- 6-21
- [x] 临时解决方案。阻塞上报开发。等待煊哥上传commit,然后在开发。
- 阅读teb算法。重点阅读构建graph，优化graph，进行perf分析。同时尝试进行优化。
- 木桶效应与解耦。
- 机器上配置perf。目前机器人无法联网，以后再尝试。
- 进电梯卡门框,1：机器人没有正对电梯,2：teb没有紧密贴合kplanner，3：由于偏向一侧，导致该侧激光点数量明显减少，接近时修正为时已晚。

- 6-22
- 凡事遵从现实,现实第一性.
- 英文阅读经济与社会变化.
- 调度，局部地图更新的问题。高cpu占用问题。梯度问题。

- 6-23
- 配置T1机器人激光雷达.下载最新的sdkeli雷达驱动,并且通过rqt_reconfige结合rviz设置屏蔽角度. done!
- 自测阻塞检测功能.临时方案 done!
- 电梯内定位微调优化. Undo!
- 进行perf分析.运行半分钟,并记录movebase的cpu占用.perf并记录数据进行分析.cpu%150~160.
- /etc/udev/70 取消eth的注释。
- /etc/network/interfaces

- 6-29
- 
