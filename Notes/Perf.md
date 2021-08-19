### knowledge
- 

### principle
- PMU,tracepoint,kernel. Event Count. 
- Task-clock-msecs: CPU utilization.
- Context-switches: switches of process cont进程切换次数，记录了程序运行过程中发生了多少次进程切换，频繁的进程切换是应该避免的。
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

### practice


