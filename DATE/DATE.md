- Acc Target Select
	- [x] Carmaker
	- [x] add short distance lane predict.
		- front wheel angle = steer angle / 14.8 
	- [x] coordinate problem.
	- [x] Test in carmaker.
	- [ ] medium distance.
		- [ ] Select traffic cars trajectories.
			- [ ] increase trajectory length to compute history delta_y. Longer obstacle detect distance 100m is perfered. Considering GuoDong's code.
			- [ ] select valid trajectories from obstacle trackers.
				- [ ] add historical_dy and same_forward_direction func in obstacle tracker.
				- [ ] add trajectories quality.
				- [ ] fusion, how to compute s, st. Pay attention.
				- logics: long enough, same direction, close in history.
				- what about New obstacle but has not goes to
		- [ ] evaluate function.
		- [ ] change lane and trajectory joint
		- [ ] 

- Acc follow target select, test data callback
	- [x] read nullmax_pilot to make filter logic clear.
		- case 1: obstacle in path id change, distance in y axis jump change for far to close. step change of pulse change.
		- case 2: lane recognization bad, driver override, 
left/right front car very close or ttc(time distance) is small.
	- [x] make needs clear.
		- take dowm date, case, bag path, bag timestamp start end. 
		- judge case according to data queue.
		- first step base on screen UI, next step base on scripts.
	- [x] base on single data folder, code filter.
	- [ ] code script to scan all directories and filter all bag, generate a index file.
	- [ ] product iteration.

- planner offline test
	- [ ] some topics need to be added.

- Freecell game
	- heuristic prior search
	- heuristic net func。 To distance。 Train step froward。
	- 

