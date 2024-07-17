## 一、准备工作
推荐在 Ubuntu 18.04 或者 Debian 10 以上的 Linux 发行版环境中运行本项目。若使用虚拟机，建议内存设置为5GB以上。
### 安装依赖
```
#更新ubuntu下载源
sudo apt update 
#安装依赖的工具和库
sudo apt install proxychains4 shadowsocks-libev vim wget git tmux make gcc time curl libreadline6-dev libsdl2-dev openjdk-11-jre zlib1g-dev flex autoconf bison sqlite3 libsqlite3-dev
```
### 安装 Java
推荐安装Java11以上的版本，网上参考资料比较丰富，请自行查阅安装。
### 安装 Mill
执行以下命令将mill安装在根目录下的bin文件夹中，注意版本号：若使用IDEA，建议安装0.11.7，否则安装0.9.7
```
#下载mill的安装脚本
sh -c "curl -L https://github.com/com-lihaoyi/mill/releases/download/0.9.7/0.9.7 > /bin/mill && chmod +x /bin/mill"
#安装mill，可能需要耗费一些时间
mill 
```
或参考[该指南的Manual部分](http://mill-build.com/mill/Installation_IDE_Support.html#_manual)，注意安装0.9.7版本
### 安装 GNU RISCV 工具链
Ubuntu 18.04 或者 Debian 10 以上:<br />`sudo apt-get install g++-riscv64-linux-gnu`
### 安装 Verilator
Ubuntu 18.04 或者 Debian 10 以上:<br />`sudo apt-get install verilator`<br />或者请参考[官方教程](https://verilator.org/guide/latest/install.html)从源文件编译安装。
### NEMU
```
cd Polaris 
git clone https://github.com/ByeBeihai/NEMU.git
echo "export NEMU_HOME=NEMU文件夹的绝对路径" >> env.sh
source env.sh
cd NEMU
make riscv64-nutshell-ref_defconfig 
make #执行完后build文件夹下会生成so文件
```
## 二、仿真运行流程
```
cd Polaris
make clean
source env.sh
make emu EMU_TRACE=1 EMU_CXX_EXTRA_FLAGS="-DFIRST_INST_ADDRESS=0x80000000" WITH_CHISELDB=01
./build/emu -b 0 -e 0 -i ./ready-to-run/microbench.bin #看到MICROBENCH PASS即为成功
./build/emu -help #该命令可查看更多emu执行选项
```
或者参考 [GitHub仓库 Readme.md 第三节](https://github.com/ByeBeihai/Polaris#3-simulation-and-fpga-implement)
## 三、IDE Support（IntelliJ IDEA）
### 1.修改build.sc
```
import mill._, scalalib._
import coursier.maven.MavenRepository

object ivys {
  val scala = "2.13.10"
  val chisel = ivy"edu.berkeley.cs::chisel3:3.6.0"
  val chiselPlugin = ivy"edu.berkeley.cs:::chisel3-plugin:3.6.0"
}

trait CommonModule extends ScalaModule {
  override def scalaVersion = ivys.scala

  override def scalacOptions = Seq("-Ymacro-annotations")
}

trait HasChisel extends ScalaModule {
  override def ivyDeps = Agg(ivys.chisel)
  override def scalacPluginIvyDeps = Agg(ivys.chiselPlugin)
}

trait CommonNS extends SbtModule with CommonModule with HasChisel

object difftest extends CommonNS {
  override def millSourcePath = os.pwd / "difftest"
}

object generator extends CommonNS {

  override def millSourcePath = os.pwd

  override def moduleDeps = super.moduleDeps ++ Seq(
    difftest
  )

  object test extends SbtModuleTests with TestModule.ScalaTest

}
```
### 2.生成.idea工程文件
```
cd Polaris
make bsp #install a BSP connection file
mill mill.idea.GenIdea/idea #生成.idea工程文件
```
启动 IDEA 打开Polaris文件夹即可自动导入依赖项，完成 chisel 编译环境配置。
## Troubleshooting
### mill编译build.sc时报错
输入`mill version`检查mill版本。0.11.7版本编译原始build.sc会报错，可参考[第三节中的build.sc](#ucxwY)进行修改或者安装0.9.7的mill，但低版本mill不支持IDEA。
### 运行emu时出现 mmap: Cannot allocate memory
一般是由于虚拟机内存设置过小，建议设置为5GB（即5120MB）以上
