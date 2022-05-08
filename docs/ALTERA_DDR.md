# DDR 
1. DDR2  
    1. Quartus DDR and DDR2 SDRAM Controllers with ALTMEMPHY  
       1. Memory Settings
          1. Memory format:  
              1. Discrete Device:分离器件  
              2. SIMM:Single In-line Memory Module,单边接触内存模块
              3. DIMM:Dual In-line Memory Module，双列直插内存模块  
              4. UDIMM:Unbuffered DIMM，无缓冲双列直插内存模块  
                  指地址和控制信号不经缓冲器，无需做任何时序调整，直接到达DIMM上的DRAM芯片。
                  没有任何缓存，因此同频率下延迟较小。  
              5. RDIMM:Registered DIMM，带寄存器的双列直插内存模块  
                  RDIMM在内存条上加了一个寄存器进行传输，减少了并行传输的距离，保证并行传输的
                  有效性。由于寄存器效率很高，因此相比UDIMM，RDIMM的容量和频率更容易提高。  
              6. LRDIMM:Load Reduced DIMM，低负载双列直插内存模块  
                  LRDIMM内存将RDIMM内存上的Register芯片改为iMB(isolation Memory Buffer)内
                  存隔离缓冲芯片，相比RDIMM，LRDIMM并未使用复杂寄存器，只是简单缓冲，缓冲降低
                  了下层主板上的电力负载，但对内存性能几乎无影响。  
          2. Memory Preset:  
              1. Output clock pairs from FPGA:FPGA输出给存储器的差分时钟对数量。  
              2. Total Memory chip selects:FPGA输出的片选信号数量。  
              3. Total Memory interface DQ width:内存数据总线宽度。  
              4. Memory burst length:突发传输长度，一次读写可以存取的数据个数。  
              5. Memory burst ordering:突发传输的顺序  
              6. Enable the DLL in the memory devices:使能存储设备内的延迟锁相环(enable)  
              7. Memory drive strength  setting:存储器驱动强度(normal)。
              8. Memory on-die termination (ODT) setting:设置内存ODT值。DDR SDRAM接口中不可用。
              9. Memory CAS latency setting:设置从读取命令到内存中的第一个输出数据的时钟周期延迟。CAS（Column Address Strobe）:列地址选通脉冲。
              10. Memory additive CAS latency setting:存储器附加的CAS 延迟设置(disabled)。
              11. Memory Vendor:存储器厂家
              12. Memory format:存储器类型
              13. Maximum memory frequency :存储器最大工作频率
              14. Column address width:存储器列地址宽度
              15. Row address width:存储器行地址宽度
              16. Bank address width:bank 地址宽度
              17. Chip selects per DIMM:DIMM 片选信号位宽
              18. DQ bits per DQS bit:一个DQS数据选通信号对应DQ数据信号的位宽
              19. Precharge address bit:预充电地址位宽  
              20. Drive DM pins from FPGA:是否使能从FPGA输出数据掩码信号(DM)
       2.  PHY Settings
       3.  Board Settings
       4.  Controller Settings
           1. Controller architecture:控制器架构(优先High Performance Controller II)
           2. Enable self-refresh controls:启用自刷新控制，打开以使控制器能够控制何时将外部内存设备置于自刷新模式
           3. Enable power down controls:启用电源关闭控制，打开以使控制器能够控制何时将外部内存设备置于电源关闭模式
           4. Enable auto power down:启用自动电源关闭，打开以使控制器能够在观察到一定数量的空闲时钟周期后自动将外部内存设备置于断电模式，用户可以指定空闲周期的数量。
           5. Auto power down cycles:自动断电周期，见1.1.4.4
           6. Enable user auto-refresh controls:启用用户自动刷新控制，打开以使控制器允许用户发起单次刷新
           7. Enable auto-precharge control:启用自动预充控制，打开以启用控制器顶层的自动预充控制信号，当请求突发读或者写时置自动预充有效，允许用户指定控制器是否在突发读写结束时关闭当前打开的页
           8. Enable Reording:启用重排，打开以允许控制器执行命令和数据重拍以达到最高效率
           9. Starvation limit for each command:每个命令的饱和限制，指定在一个等待命令送达前可以送达的命令个数，合法值为1-63
           10. Local-to-memory address mapping:本地到内存的映射，允许用户控制 Avalon接口上的地址位与内存接口上的chip, row, bank, column位之间的映射。如果用户的应用程序发出大于内存设备列大小的突发问题，请选择 Chip-Row-Bank-Column 选项。此选项允许控制器使用预先bank管理功能来隐藏当突发传输到达列末端时改变当前打开行的效果。另一方面，如果用户的应用程序有几个主设备，每个都使用单独的存储器区域，请选择Chip-Bank-Row-Column选项。此选项允许用户使用顶部地址位将内存中的物理库分配给每个主设备。物理bank分配避免了不同的主设备访问同一bank可能导致的效率低下问题，因为控制器必须随后打开和关闭同一个bank。
           11. Command queue look-ahead depth:命令队列预先深度，设定该值以控制预先bank管理逻辑需要检查的读写请求数量。
           12. Local Maximum Burst Count:本地控制器最大读写突发长度
           13. Reduce controller latency by :减少控制器延迟量
           14. Enable configuration and status register interface :启用配置和状态寄存器接口
           15. Enable error detection and correction logic:启用错误检测和纠正逻辑
           16. Enable auto error correction:启用自动错误纠正
           17. Multiple controller clock sharing:多控制器时钟共享
           18. Local interface protocol:本地接口协议

[参考资料](https://blog.csdn.net/huan09900990/article/details/78363054)
