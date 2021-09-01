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
	- [ ] read topic
	- [ ] read config
	- [ ] write data into planning_context
	- [ ] how to run?
- tips
	- according to aebs, maybe planner_node no need to run start(). !!!