### Principle
new a population
loop
	- ***dropout*** : compute **fitness** and dropout bad individuals. 
	- ***crossover*** : survived individuals crossover to reproduction new generation with **genetic**.
	- ***mutate*** : new generation mutate to create new genetic.

### Trick
- dropout can use roulette random to bring random in.
- elites should be retained.
- genetic should be smart design to reduce complexity. mutate should be wide. crossover should pass good genetic. fitness should be able to compare tow individuals.
- to keep population diversity, use "niche penalty". if a group of individuals sufficient similarity, give a penalty.
- introduce new generated "random immigrants"
into gene pool.

### Characteristic
- if all is random, GA same as random search. ***Heuristic infomation*** comes from ***crossover*** and ***fitness***. Either fitness will figure out evolution direction, or crossover will creat bettter generation. 
- If crossover can do that, fitness no need to have good gradient. Only required capable in statistic.
- genetic encode will bring a huge and powerful mutate.
- fitness must not be exaggeration terrible!
- population brings collective intelligence. And distruibutable computation.
- population brings robust random.
- GA can search for a "good" solution very fast.
- default to fit dynamic environment?? because population deversity decrease to converge.