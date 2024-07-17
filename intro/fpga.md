# 基于Xilinx XC7K70T的开源最小系统构建指南
## 一、准备工作
### Vivado
推荐在Vivado 2018.3上运行本项目，若Vivado版本高于2019.2需要安装Vitis。为了方便各位同学的安装，以下是Vitis2020.2安装包的夸克网盘链接，建议预留100GB的磁盘存储空间。（注：Vitis内含Vivado软件）<br />链接：[https://pan.quark.cn/s/e5dac7715580](https://pan.quark.cn/s/e5dac7715580)
### BitStream、RT-Thread.bin
请下载该链接中的文件到方便寻找的位置<br />链接：[https://pan.quark.cn/s/87c2e952fdb7](https://pan.quark.cn/s/87c2e952fdb7)
## 二、烧录BitStream文件
### Open HardWare Manager
![image.png](https://github.com/CallWoa/OpenBPU2-doc/blob/master/image/fpga1.png?raw=true)
### Auto Connect
将开发板通过Xilinx下载器连接电脑，点击Auto Connect。若无法连接开发板-localhost(0)，一般是由于未安装驱动，请自行检索网页资料进行安装解决。<br />![image.png](https://github.com/CallWoa/OpenBPU2-doc/blob/master/image/fpga2.png?raw=true)
### Program Device
点击Program Device，选择准备好的BitStream文件，点击Program<br />![image.png](https://github.com/CallWoa/OpenBPU2-doc/blob/master/image/fpga3.png?raw=true)<br />![image.png](https://github.com/CallWoa/OpenBPU2-doc/blob/master/image/fpga4.png?raw=true)
## 三、启动RT-Thread
### 打开Vivado Tcl Shell
![image.png](https://github.com/CallWoa/OpenBPU2-doc/blob/master/image/fpga5.png?raw=true)
### 通过XSCT启动RT-Thread
```
xsct #进入Xilinx Software Command Line Tool
connect
ta 2
cd rtthread2024.bin所在文件夹的绝对路径 #例如E:/Proc/Polaris
dow -data rtthread2024.bin 0x0
jtagterminal -start
```
![image.png](https://github.com/CallWoa/OpenBPU2-doc/blob/master/image/fpga6.png?raw=true)<br />按下S2按钮复位系统，启动RT-Thread<br />![image.png](https://github.com/CallWoa/OpenBPU2-doc/blob/master/image/fpga7.png?raw=true)
