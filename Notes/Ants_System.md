### Principle
- as for now, we regard AS algorithm is only capable to solve problems which can be tranformed to "fing shortest path in graph problem".
- new agents and loop
	- ***move***
	- ***info***
- agent decide its move with randomly with info like "trajectory momentum", "heuristic info to goal", "info shared with agents".
- once agent got reward, give more precise info. For example, if reach goal, info trajectory should be enhanced. if got stuck, give penalty to trajectory to tell others got away(or jail for some time to punish). if reach goal, should "rest" as long as path length, to make long path less info.
 
### Trick
- use "math model" mind to judge if a problem can be transfromed into "graph problem".

### Characteristic
- high risk of stop converge!
- low search efficient!
- high efficiency to  high precise!
- 
