# 总体架构
## 处理器核特性
- Instruction Sets: RV64IMACP
- Privileged Mode: U/S/M
- Virtual Memmory: SV39
- Issue Num: 2(single-issue supported as well)
- Cache: 32KB DCache + 32KB ICache + 128KB L2 Cache

## 处理器核架构
北极星处理器是顺序双发射结构设计。它采用变长流水线的后端结构来平衡每个条指令的效率和时序。整个处理器的流水线最长可以达到 8 级。<br />Polaris 的整体结构图如下，其中灰色部分不属于本设计的工作:

![image.png](https://github.com/CallWoa/OpenBPU2-doc/blob/master/image/arch.png?raw=true)

具体结构设计详见对应章节的介绍。
