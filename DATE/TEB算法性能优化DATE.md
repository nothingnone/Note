- 6-24
### 初始测试
move_base cpu占用150%~160%

42% Costmap::updateMap
- 25% InflaLayer::updateCosts
	- 21% InflationLayer::enqueue
		- 12% CellData::lessId::pair 
- 13% memset

12% executeCB
- 11% teb_local_plannerROS::computeVelocityCommands
	- 6% TebOptimalPlanner::checkTrajectoryHealthy

7% KPlannerROS::makePlan(PoseStamped::vector)
	- 3% KPlanner::calcKPlannerDijkstra

22% g2o(teb性能并不达标0.12s)
- 2% teb_local_planner::EdgeAcceleration::computeError

- 总结
costmap的memset有问题.预计取消local的膨胀层,能够减少10%.

### 明确规划频率，控制频率
kplanner 全局10 
teb 全局 局部

### perf对锁进行分析
学习

