# MIG7

## 1. 生成IP核
1. 首页
   
   ![image-20211207084229307](.\docs\assets\XILINX_MIG7.assets\image-20211207084229307.png)

2. 选择创建新设计，设置IP核名称

   ![image-20211207084751937](.\docs\assets\XILINX_MIG7.assets\image-20211207084751937.png)

3. 下一步

   ![下一步](.\docs\assets\XILINX_MIG7.assets\image-20211207084945693.png)

   ![选择FPGA型号](.\docs\assets\XILINX_MIG7.assets\image-20211207085302542.png)

4. 选择DDR3 SDRAM类型

   ![image-20211207085415430](.\docs\assets\XILINX_MIG7.assets\image-20211207085415430.png)

5. 根据内存的手册设置时钟、内存类型、内存编号

   ![image-20211207094804038](.\docs\assets\XILINX_MIG7.assets\image-20211207094804038.png)

   设定自定义的内存参数

   ![image-20211207094107132](.\docs\assets\XILINX_MIG7.assets\image-20211207094107132.png)

6. 设置其他选项

   ![image-20211207095445302](.\docs\assets\XILINX_MIG7.assets\image-20211207095445302.png)

   - Input Clock Period为系统输入时钟，可选的值取决于第5步内存频率的值。

     该时钟输入到IP核内部的锁相环，生成内存所需时钟。

   - Memory Address Mapping Selection为用户接口地址线到内存地址线的映射关系

   - 其他选项根据内存手册设置

7. 设置UI接口时钟、参考时钟类型
   
   ![image-20211207100101969](.\docs\assets\XILINX_MIG7.assets\image-20211207100101969.png)
   
   两个时钟说明如下（7 Series FPGAs Memory Interface Solutions,UG586::page146 October 16, 2012）
   
   ![image-20211207090120703](.\docs\assets\XILINX_MIG7.assets\image-20211207090120703.png)
   
   Debug信号根据需要选择是否启用
   
8. 设置其他选项

   ![image-20211207101823454](.\docs\assets\XILINX_MIG7.assets\image-20211207101823454.png)

9. 选择引脚分配方式

   ![image-20211207102114653](.\docs\assets\XILINX_MIG7.assets\image-20211207102114653.png)

   - New Design：用于还未确定内存与FPGA IO引脚连接关系的情况，由生成工具自动分配合适的引脚，再由此设计硬件。

     如下图所示，只需要选择对应的引脚分配在哪个Bank

     ![image-20211207102539629](.\docs\assets\XILINX_MIG7.assets\image-20211207102539629.png)

   - Fixed Pin Out：用于已经确定内存与FPGA IO引脚连接关系的情况，根据原理图设置引脚分配。

     手动选择为每个引脚的创建IO约束，或者从sdc/ucf文件批量导入IO约束。

     需要验证IO约束是否有效

     ![image-20211207102708456](.\docs\assets\XILINX_MIG7.assets\image-20211207102708456.png)

10. 选择系统时钟引脚位置和其他可选引脚

    在第7步中参考时钟不选择和系统时钟相同的话，此处需要指定参考时钟引脚位置

    ![image-20211207103038427](.\docs\assets\XILINX_MIG7.assets\image-20211207103038427.png)

## 2. 验证和重新配置引脚

1. 首页

   ![image-20211203142502524](.\docs\assets\XILINX_MIG7.assets\image-20211203142502524.png)


2. 选择验证引脚和更新设计

   ![image-20211203142636095](.\docs\assets\XILINX_MIG7.assets\image-20211203142636095.png)

3. 选择IP核位置和约束文件位置

   ![image-20211203142848092](.\docs\assets\XILINX_MIG7.assets\image-20211203142848092.png)

4. 设置引脚并验证

   ![image-20211207083243891](.\docs\assets\XILINX_MIG7.assets\image-20211207083243891.png)

5. 设置用户接口时钟

   ![image-20211207083554795](.\docs\assets\XILINX_MIG7.assets\image-20211207083554795.png)

