# 代码讲解视频

## 视频简介
- IDU：该视频主要讲解了译码级的代码。译码级代码主要包括了Decode.scala、IDU.scala 以及 isa文件夹，其中Decode.scala包含了指令类型、运算器、源操作数类型的编号定义以及指令译码表的注册；IDU.scala是译码级的顶层，isa文件夹中包含了所有指令的译码表。
- ISU：该视频主要讲解了发射级SIMD_ISU.scala的代码。发射级中的数据依赖检测采用的是记分牌算法，维护了两个硬件结构: 指令环形队列和寄存器使用表，视频包含了该部分硬件的逻辑原理以及代码实现的讲解。
- EXU：该视频主要讲解了执行级SIMD_EXU.scala的代码。SIMD_EXU.scala是整个执行级的顶层，包含了所有运算器的调用和信号通道的连接，其中涉及到了LSU和CSRU之间的一些特殊逻辑。
- WBU：该视频主要讲解了写回级SIMD_WBU.scala和Backend.scala的部分代码。SIMD_WBU是整个写回级的顶层，其中包含了32个整型通用寄存器和32个浮点通用寄存器以及两类通用寄存器的读写逻辑。Backend.scala是整个北极星后端的顶层，其中包含了ISU、EXU、WBU的连接逻辑，EXU的输出通道的数量等于后端中包含的运算器的数量，WBU的接收通道的数量设定为3，二者之间的连接匹配逻辑在视频中也稍作了讲解。
- Backend：该视频主要讲解了北极星后端顶层文件Backend.scala的代码。Backend作为北极星后端的顶层模块，即后端母模块，包含了三个主要成员，分别是ISU、EXU和WBU。该模块主要定义了上述三个流水级模块之间的连接匹配逻辑，整体采用的是顺序发射，顺序执行，顺序写回的方案。

## 视频链接及二维码
此处放置了代码讲解视频的百度网盘链接和二维码，有需要的同学可以自行下载。由于讲解者本人也尚处代码学习阶段，如有疏漏，还请多多包涵指正。<br />链接: [https://pan.baidu.com/s/1ZWS-ciWraP_DLyDM6eHO7g?pwd=2qvr](https://pan.baidu.com/s/1ZWS-ciWraP_DLyDM6eHO7g?pwd=2qvr) 提取码: 2qvr

![image.png](https://github.com/CallWoa/OpenBPU2-doc/blob/master/image/code.png?raw=true)
## <br />
