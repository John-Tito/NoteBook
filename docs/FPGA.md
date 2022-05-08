# 大纲
[TOC]

# 逻辑  
数字电路基础

# 语言  
1. VHDL  
	1. 几种移位操作：  
      ```vhdl
      1. Y1 = (Y1 srl 1); --逻辑右移,左侧填充'0'
      2. Y1 = (Y1 sra 1); --算数右移,左侧填充符号位
         VHDL 93标准支持,操作数类型:bit_vector
      3. Y1 <= shift_right(Y1, 1);
         需要调用ieee.numeric_std包
      4. Y1 = Y1(Y1'left) & Y1(Y1'left - 1 downto 1);
      5. Y1 = Y1(X) & Y1(X - 1 downto 1);
         常规移位操作
      ```
2. SystemVerilog/Verilog  
   1. package  
      ```vhdl
      SystemVerilog中的 package提供了保存和共享数据、参数和方法的机制，可以在多个 module、 class、 program和 interface中重用。
      package中声明的内容都属于这个 package作用域（scope）。在使用这些内容时，需要先 import这个 package，然后通过 package引用。
      SystemVerilog中的 package通过 package和 endpackage声明。
      ```

# 接口/总线/协议
1. UART
3. CAN
4. IIC
5. SPI
5. LVDS
   <details>
      <summary>LVDS INFO</summary>
      <pre>
         1. LVDS（Low Voltage Differential Signal）即低电压差分信号.
         2. LVDS的特点是电流驱动模式 , 电压摆幅350mV加载在100Ω电阻上.
      </pre>
   </details>
6. USB
7. Eth
8. [DDR](.\DDR.md)  
9. [PCIE](.\PCIE.md)  
10. AVALON总线
    symbol：最小寻址单位
    byteenable:寻址字节
11. AXI总线  

# 模块/IP
1. RAM
2. FIFO
3. PLL
4. ETH
5. [DDR](.\DDR.md) 

# 芯片
1. SRMA
2. FLASH
3. ETH/PHY

# FPGA原理
1. Xilinx
   1. 架构

   2. 资源

   3. I/O BANK

      1. 高性能（HP）I/O Bank

         HP I/O Bank：最大VCCO 1.8V，差分信号电平LVDS

      2. 宽压范围（HR）I/O Bank

         支持最大VCCO 电压为3.3V，差分信号电平LVDS_25

   4. 内核电压
      1. 48nm工艺 1.2V
      2. 28nm工艺 1.0V
   5. spartan-6配置模式
      1. slaveSelectMAP
        1.
2. Altera
   1. 速度等级：
      1. CYCLONE IV E  
         商用器件：-6(最快),-7,-8,-8L,-9L  
         工业器件：-8L  
         拓展工业器件/自动化器件：-7  
      2. CYCLONE IV GX  
         商用器件：-6(最快),-7,-8  
         工业器件：-7  
   2. 内核电压
      1. CYCLONE IV E
         1. 1.2V
         2. 1.0V 后缀L
         3. 后缀命名规则![后缀命名规则](.\docs\assets\FPGA.assets\image-20201228195746996.png)

# 约束
   1. 时序约束
   2. I/O约束

# 设计
   1. 复位
      1. 同步复位
      2. 异步复位
      3. 异步复位+同步释放 ~~同步复位+异步置位~~
      4. 异步FIFO的复位信号
   2. 同步通信
      1. 系统同步
         不同IC使用同一个公共时钟，通信双方根据该时钟进行数据收发操作。
      2. 源同步
         发送IC生成发送时钟，并根据该时钟进行数据发送，接收IC根据该时钟进行数据接收，数据线与时钟线必须严格一致。
      3. 自同步
         发送IC生成包含时钟和数据数据流。  
      4. SerDes（serialize and deserialize）/MGTs （Multi Gbit Transceivers  
         1. 构成
            1. PCS (物理编码子层)
               1. 编码器
               2. 解码器
            2. PMA (物理介质适配层)
               1. PISO（并串转换/串行化模块）
               2. SIPO（串并转换/解串行化模块）
            3. PMD (物理介质关联层)
               1. 串行发送线
               2. 串行接收线
            4. PLL (时钟管理)
         2. 特点
            1. 串行差分传输
            2. CDR技术
               1. 使用PLL来进行时钟恢复
            3. 预加重,均衡
               1. 发送端使用FFE(Feed forward equalizers)结构
   3. 异步通信
   4. 状态机
      1. 格雷码：相邻之间只变1bit，编码密度高。
      2. 独热码：任何状态只有1bit为1，其余皆为0，编码密度低。
   5. 跨时钟域处理
      1. FIFO
      2. 握手信号
      3. 打两拍消除亚稳态
   6. [静态时序分析](.\STA.md)


# 算法
1. 算法设计
   1. 性能指标
      $$
      T≥(T_{co}+ T_{logic}+T_{routing}+T_{su}−T_{skew}
      $$
   2. 系统时钟频率  
         $$F_{max}≥{1\over(T_{co}+T_{logic}+T_{routing}+T_{su}−T_{skew}})$$  
         $T_{co}$：发端寄存器时钟到输出时间，取决于芯片工艺  
         $T_{logic}$：组合逻辑延迟，主要影响因素为代码风格  
         $T_{routing}$：两级寄存器间布线延迟，主要影响因素为布局布线策略  
         $T_{su}$：收端寄存器建立时间，取决于芯片工艺  
         $T_{skew}$：两级寄存器时钟歪斜，时钟同一边沿到达两个寄存器时钟端口的时间差，在同步设计中可忽略  
         $T_{jitter}$ ：时钟抖动，时钟质量的体现  
   3. 迟滞Latency  
      数据从输入端口到达输出端口的时间，表示系统每次操作所需要的时间  
   4. 数据吞吐量Throughput  
      相邻两次数据输入的时间间隔，表征系统对数据输入的接收和处理能力  
   5. 数据率DataRate  
      系统时钟频率除以数据吞吐量，表示数据输入速率  
   6. 数据格式  
      1. 整数  
      2. 浮点数  
         构成：符号位（Sign Bit）、尾数（Mantissa）、基数（Radix）、指数（Exponent）  
         $$
            n=(−1)^S×M×R^e
         $$
         规格化：E不全为0，也不全为1  
         $$
            \left\{\begin{array}{} e=|E|-bias\\bias=2^{k-1}-1\end{array}\right.
         $$
         $$
            n=(-1)^S×|1.M|×2^{|E|-127}
         $$
         1. 单精度浮点数  
            |      31       |   30..23    |               22..0               |
            | :-----------: | :---------: | :-------------------------------: |
            |    符号位     |   指数位    |              尾数位               |
            |       S       |      E      |                 M                 |
            | 0:正数1：负数 | 偏移量：127 | 规格化：\|1.M\| 非规格化：\|0.M\| |
         2. 双精度浮点数  
      3. 定点数
2. 数字信号处理
3. 数字图像处理
4. 加密/校验算法
   1. 8B/10B
      原始数据: HGFEDCBA
      低五位: EDCBA -> abcdei
      高三位: HGF -> fghj
      编码数据: jhgfiedcba
      发送顺序: LSB(a -> j)
5.  HLS
	1. Quartus HLS Compiler 必要的工具和操作：
		1. ModelSim FPGA Edition/ModelSim FPGA Starter Edition
		2. 将 ModelSim\* 的路径添加为您的PATH环境变量
		3. Microsoft Visual Studio 2017 Professional/Community
		4. Quartus Prime
		5. HLS Compiler
		6. 每次都需要以管理员身份初始化 Intel HLS Compiler Pro Edition环境
	2. SystemGenerator
		1. 同时打开Vivado和MATLAB
		2. 使用MATLAB进行算法实现(使用硬件编程思路)
		3. Simulation建模(添加SystemGenerator和其他组件)
	3. DSP_Builder

# 工具
1. 软件
   1. quartus
      1. signalTap  
   2. vivado
   3. TCL脚本语言
   4. Linux命令
   5. ARM系统
   6. 嵌入式系统
   7. IDE
   8. GIT/SVN
2. 硬件
   1. 逻辑分析仪
   2. 频谱分析仪
   3. 示波器
   4. 信号发生器

# 应用
1. 通信
   $dB = 10 log_{10}^{P}$ or $dB = 20 log_{10}^{P}$
2. 深度学习/神经网络/人工智能
3. 图像/视频/视觉
4. 无人驾驶
5. 军工