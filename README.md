# 欢迎访问北极星官方文档！  
这是北极星的官方文档仓库，包括北极星项目的整体介绍、代码仓库概览、上手教程、处理器核介绍、开发工具链介绍等内容。

> **什么是北极星？About Polaris**  

> 本设计按照 RISC-V Packed SIMD 指令集(以下简称 P 扩展或 RVP)的最新标准 v0.9.11，基于 NutShell 的开发框架，复用其部分运算部件和前端部件，实现一款顺序双发射超标量处理器后端，应用后端的新处理器代号为“北极星”(全称 “支持 RVP 的 SIMD 双发射超标量处理器”，以下简称其英文代号“Polaris”)。该 后端可以与 NutShell 的前端协同工作，支持 RISC-V64 IMACP 指令集，为 RISC-V 开源社区提供 P 扩展的实现参考以及高能效比的指令集扩展平台。
本设计作为本课题组的开源项目的一部分，还将与组内所开发的双发射前端对接，使 Polaris 最终完善为一款支持 RVP 的 SIMD 双发射超标量处理器。

## 北极星项目链接
- Polaris 代码仓库: [https://github.com/ByeBeihai/Polaris](https://github.com/ByeBeihai/Polaris)
- Polaris 文档仓库: [https://callwoa.github.io/OpenBPU2-doc/](https://callwoa.github.io/OpenBPU2-doc/)
- Nexus-AM 编译平台: [https://github.com/ByeBeihai/nexus-am](https://github.com/ByeBeihai/nexus-am) 
- FPGA 验证框架: [https://github.com/ssdfghhhhhhh/NutShell_U250](https://github.com/ssdfghhhhhhh/NutShell_U250) 
- Polaris指令集扩展简易教程: [https://github.com/ByeBeihai/Polaris/blob/master/extension.md](https://github.com/ByeBeihai/Polaris/blob/master/extension.md)
## 北极星仓库目录结构
项目 Repository 建立在 Scala 框架下, 其中主要的的目录和文件如下：
```
.
├── debug/             # 处理器核测试脚本
├── fpga/              # 用于FPGA平台调试运行的相关文件
├── project/           # 构建SBT项目的相关配置文件
├── src/               # 处理器核源代码
├── script/            # 其他脚本文件
├── tool/              # 其他工具
├── Makefile           
└── README.md          # 项目介绍
```
./src 下的文件是项目最核心的处理器核源代码, 简要说明如下：
```
./src
  ├── main/scala
  │    ├── bus         # 总线相关
  │    ├── device      # 输入输出设备相关
  │    ├── nutcore     # 核心相关
  │    ├── sim         # 仿真相关
  │    ├── system      # 外围系统
  │    ├── top         # 项目顶层文件及配置文件
  │    └── utils       # 工具相关
  └── test
       ├── csrc        # C++测试文件, 主要用于Verilator仿真项目构建
       ├── vsrc        # Verilog测试文件
       └── scala       # Scala测试文件
```


<!-- ## 目录
- ### 简介  
    - FPGA构建指南  
    - 北极星项目导引  
    - 快速上手教程  
    - 代码讲解视频  
- ### 处理器核介绍
    - 总体架构
    - 后端
        - 总体架构  
        - 流水线结构  
            - 发射级  
            - 执行级  
            - 写回级
        - 后端部件
            - PEXTU  
            - CSRU
            - LSU
            - TLB
            - ALU & BRU
            - MDU -->
