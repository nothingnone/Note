- 6-24
初始设置
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
	- 3% [KPlanner::calcKPlannerDijkstra

22% g2o
- 2% teb_local_planner::EdgeAcceleration::computeError

规划频率
kplanner 全局
teb 全局 局部
