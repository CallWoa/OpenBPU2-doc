# LSU

LSU 使用 SimpleBus 总线协议，由两部分组成:通用流水级 LSU_PIPE 和用于处理原子指令的 LSU_ATOM。 

![image.png](https://github.com/CallWoa/OpenBPU2-doc/blob/master/image/LSU.png?raw=true)

LSU_PIPE 由 3 级流水组成，第一级流水负责完成 req 请求的握手，第二级 流水负责完成 resp 请求的握手，第三级流水为可选流水，当访存出现异常时，指 令将进入第三级流水，并将 LSU 标记为不可传入新指令，向 EXU 级传出异常信 息，待 EXU 模块将其交由 CSRU 进行处理。对于没有发生异常的处理，允许其 直接从第二级流水连入 LSU 的提交端口等待指令提交。 <br />LSU_ATOM 复用 NutShell 的多周期原子指令访存逻辑，分多个周期完成原 子指令，在执行周期结束后，其被允许连接至 LSU 的提交端口进行指令提交。为了保证原子指令的原子性，当 LSU_ATOM 工作时，新的指令将不被允许进入LSU 内，直到 LSU_ATOM 内的指令成功提交。<br />流水线 LSU 相比于原版 NutShell 的 LSU，实现了从多周期 LSU 到流水线 LSU 的升级，在密集访存场景下可以获得更高的性能表现。但由于 RISC-V 架构 本身的限制 [1]，LSU 的单次访存只能取回最长 64bit 的数据，一定程度上限制了 向量化程序的性能表现。<br />LSU 在之后的工作中可以通过以下方式增强访存能力: 

1. 为 LSU 增加 SIMD 指令集扩展，允许 LSU 进行超长宽度数据的存取， 以及允许 LSU 以更多模式进行访存(例如使用固定步长访问非连续的内存地址 空间)以加速在矩阵等多维数据场景的表现。 
2. 配合 Cache 进行接口优化改造，允许 LSU 通过多端口向 LSU 发出存取 请求，扩大 LSU 的访存带宽。
3. 扩充 LSU 的结构，为其设置访存队列，并允许在 LSU 内部进行数据前 递以减少访存频次与访存延迟。 