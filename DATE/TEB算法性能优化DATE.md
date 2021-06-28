- 6-24
### perf 安装与符号解析


### 初始测试
move_base cpu占用150%~160%

42% Costmap::updateMap
- 25% InflaLayer::updateCosts
	- 21% InflationLayer::enqueue
		- 12% CellData::lessId::pair 
- 13% memset

12% executeCB
- 11% teb_local_plannerROS::computeVelocityCommands:2%
	- 6% TebOptimalPlanner::checkTrajectoryHealthy

7% KPlannerROS::makePlan(PoseStamped::vector)
	- 3% KPlanner::calcKPlannerDijkstra

22% g2o(teb性能并不达标0.12s)
- 2% teb_local_planner::EdgeAcceleration::computeError
- 2.62% TebOptimalPlanner::buildGraph

- 总结
costmap的memset有问题.预计取消local的膨胀层,能够减少10%.global的costmap的更新频率有问题,如果是20Hz问题就很大.costmap的整体占用都有问题.
teb的占用更大,因为teb的频率与实际有差.g2o的计算量难以下降.
teb的速度计算有问题,占用过大.
teb的buildgraph只占用了2.62%

### 明确规划频率，控制频率
kplanner 全局10 
teb 全局 局部
- 总结

### perf对锁进行分析
- 学习
缺省情况下，除了 task-clock-msecs 之外，perf stat 还给出了其他几个最常用的统计信息：
Task-clock-msecs：CPU 利用率，该值高，说明程序的多数时间花费在 CPU 计算上而非 IO。
Context-switches：进程切换次数，记录了程序运行过程中发生了多少次进程切换，频繁的进程切换是应该避免的。
Cache-misses：程序运行过程中总体的 cache 利用情况，如果该值过高，说明程序的 cache 利用不好
CPU-migrations：表示进程 t1 运行过程中发生了多少次 CPU 迁移，即被调度器从一个 CPU 转移到另外一个 CPU 上运行。
Cycles：处理器时钟，一条机器指令可能需要多个 cycles，
Instructions: 机器指令数目。
IPC：是 Instructions/Cycles 的比值，该值越大越好，说明程序充分利用了处理器的特性。
Cache-references: cache 命中的次数
Cache-misses: cache 失效的次数。
- trace
- slab 分配器
- 编译-g，减少影响调试的优化。倘若对性能影响很大，说明编译器的优化幅度较大，亦从侧面表明有bad code。

- 关于对锁的分析,目前的结果是:
perf 只能够对内核锁进行分析,并且需要编译内核时支持相关选项.
valgrind 似乎对性能影响太大，不建议使用.DRD与Helgrind工具.
^ mutrace 首先在测试程序中验证.注意测试其是否必须程序自动退出.
^ print 如何打印并收集信息.并编写脚本进行数据处理.

### 6-25 优化与测试
- 原始数据 高负载时占用150%，长路线规划初始段，以及峰值可达190%
- 对checkTrajectoryHealthy的average进行优化后，由150降到142. Done!
- 降低全局costmap由20Hz降低到10Hz，占用高负载110%，峰值160%.不影响运动表现，但会导致kplanner报错，not init。

### 频率明确
原
- global_costmap: update 20, publish 10
- local_costmap : update 20, publish 5
- 

