# SODIMM:

1. SODIMM内存标识

> "204-Pin DDR3 SDRAM Unbuffered SO-DIMM Design Specification"规定的 DDR3 “End-User” DIMM类型统一的标签格式:
>
> ggggg eRxff PC3-wwwwwm-aa-bb-ccd
>
> 1. ggggg: 模块总容量，以字节为单位
> 
>    256MB, 512MB, 1GB, 2GB, 4GB等等。
> 
> 2. eR: 安装的颗粒排列数（rank）
>    1R: 1rank DDR3 SDRAM
> 
>    2R: 2rank
> 
>    4R: 4rank
> 
> 3. xff: 内存条上单个DDR3 SDRAM颗粒的数据位宽（也叫Device organization）
> 
>    x4: x4 organization, 即4位
> 
>    x8: x8 organization
> 
>    x16: x16 organization
> 
> 4. wwwww: 带宽，单位为MB/s，对于数据总线64bit，这个也可认为代表了不同的工作频率。
> 
>    6400: = 6.40 GB/s, (PC3-800 SDRAM, 数据总线8字节宽)
> 
>    8500: = 8.53 GB/s, (PC3-1066 SDRAM, 数据总线8字节宽)
> 
>    10600: = 10.66 GB/s, (PC3-1333 SDRAM, 数据总线8字节宽)
> 
>    12800: = 12.80 GB/s, (PC3-1600 SDRAM, 数据总线8字节宽)
> 
> 5. m:类型，字面意思，包含有无缓存、寄存器，尺寸等类型
> 
>    E:无缓冲Unbuffered DIMM (“UDIMM”)，带ECC(x72位模块数据总线)
> 
>    F: 全缓冲Fully Buffered DIMM (“FB-DIMM”)
> 
>    M: Micro-DIMM
> 
>    R: Registered DIMM (“RDIMM”)
> 
>    S: Small Outline DIMM(“SO-DIMM”)
> 
>    U: 无缓冲DIMM (“UDIMM”)，无ECC(x64位模块数据总线)
> 
>    一般板卡要用DIMM形式的SDRAM，用的也是SO-DIMM，小型DIMM。
> 
> 6. aa: DDR3 SDRAM 最大工作频率时钟的CAS延迟
> 
> 7. bb: 用于此DIMM的JEDEC SPD修订编码和添加级别
> 
> 8. cc: 设计使用的参考设计(如适用)
> 
>    A: 使用规范给出的参考设计:raw card ‘A’
> 
>    B: 使用规范给出的参考设计:raw card ‘B’
> 
>    AV: 使用规范给出的参考设计:raw card ‘AV’
> 
>    ZZ: 未使用规范给出的参考设计
> 
> 9. d: 所使用的参考设计的修订编号
> 
>    0: 初始发行版
> 
>    1: 第一次修订
> 
>    2: 第二次修订
> 
>    P: 预发布或工程示例
> 
>    Z: 当字段cc = ZZ时使用
> 
>    ————————————————
> 
>    版权声明:本文为CSDN博主「w0shishabi」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
> 
>    原文链接:https://blog.csdn.net/lum250/article/details/121599417

2. 内存颗粒标识

> ![三星内存颗粒丝印代码](.\docs\assets\DDR.assets/DDR存储器丝印.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAdzBzaGlzaGFiaQ==,size_17,color_FFFFFF,t_70,g_se,x_16#pic_center)
>
> ————————————————
> 版权声明:本文为CSDN博主「w0shishabi」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
> 原文链接:https://blog.csdn.net/lum250/article/details/121599417

3. 举例:

   <u>1GB 1Rx8 PC3 - 10600S - 09 - 10 - ZZZ</u>:

   1GB, 1rank,DDR3 SDRAM, x8 organization, 10.66 GB/s, (PC3-1333 SDRAM, 数据总线8字节宽)   

   Small Outline DIMM(“SO-DIMM”), CAS延迟 09, JEDEC SPD修订编码和添加级别 10

   未使用规范给出的参考设计,未使用规范给出的参考设计

   <u>K4B1G08046F</u>:

   SAMSUNG Memory, DRAM, DDR3 SDRAM, 1Gb, x8, 4 Banks, SSTL(1.5V,1.5V), 7th Gen