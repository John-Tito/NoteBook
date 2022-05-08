# MIG7

## 1. 创建IP核

   ![1](.\docs\assets\XILINX_MIG6.assets\1.png)

## 2. 选择型号

   ![2](.\docs\assets\XILINX_MIG6.assets\2.png)

## 3. bank与类型选择

   ![3](.\docs\assets\XILINX_MIG6.assets\3.png)

## 4. 选择时钟频率与内存型号

   ![4](.\docs\assets\XILINX_MIG6.assets\4.png)

## 5. 选择存储器设置

   ![5](.\docs\assets\XILINX_MIG6.assets\5.png)

   ![5-1](.\docs\assets\XILINX_MIG6.assets\5-1.png)

   在存储器的ZQ 和 VSSQ(GND)之间需要有240Ω ±1%的电阻

## 6. 选择端口类型以及地址线设置

   ![6](.\docs\assets\XILINX_MIG6.assets\6.png)

## 7. 仲裁算法选择

   ![7](.\docs\assets\XILINX_MIG6.assets\7.png)

## 8. 选择 FPGA 配置

   ![8](.\docs\assets\XILINX_MIG6.assets\8.png)

## 9 模块端口及属性

```VHDL
component ddr_mig
        generic (
            C3_P0_MASK_SIZE       : INTEGER := 8;                 -- 掩码大小,一般为端口宽度字节数
            C3_P0_DATA_PORT_SIZE  : INTEGER := 64;                -- 数据端口位宽,比特数
            C3_P1_MASK_SIZE       : INTEGER := 8;                 -- 同C3_P0
            C3_P1_DATA_PORT_SIZE  : INTEGER := 64;                -- 同C3_P0
            C3_MEMCLK_PERIOD      : INTEGER := 2500;              -- MIG IP工作的时钟周期2500 ps
            C3_RST_ACT_LOW        : INTEGER := 0;                 -- 低电平复位
            C3_INPUT_CLK_TYPE     : STRING  := "DIFFERENTIAL";    -- 输入时钟类型
            C3_CALIB_SOFT_IP      : STRING  := "TRUE";            -- DDR 校准软IP使能
            C3_SIMULATION         : STRING  := "FALSE";           -- 仿真使能，缩减仿真时间
            DEBUG_EN              : INTEGER := 1;                 -- 调试端口
            C3_MEM_ADDR_ORDER     : STRING  := "ROW_BANK_COLUMN"; -- 地址位序
            C3_NUM_DQ_PINS        : INTEGER := 16;                -- DQ引脚数量
            C3_MEM_ADDR_WIDTH     : INTEGER := 15;                -- 地址线宽度
            C3_MEM_BANKADDR_WIDTH : INTEGER := 3                  -- BANK地址宽度
        );
        port (
            -- dram
            mcb3_dram_dq      : inout STD_LOGIC_VECTOR(C3_NUM_DQ_PINS - 1 downto 0);
            mcb3_dram_a       : out STD_LOGIC_VECTOR(C3_MEM_ADDR_WIDTH - 1 downto 0);
            mcb3_dram_ba      : out STD_LOGIC_VECTOR(C3_MEM_BANKADDR_WIDTH - 1 downto 0);
            mcb3_dram_ras_n   : out STD_LOGIC;
            mcb3_dram_cas_n   : out STD_LOGIC;
            mcb3_dram_we_n    : out STD_LOGIC;
            mcb3_dram_odt     : out STD_LOGIC;
            mcb3_dram_reset_n : out STD_LOGIC;
            mcb3_dram_cke     : out STD_LOGIC;
            mcb3_dram_dm      : out STD_LOGIC;
            mcb3_dram_udqs    : inout STD_LOGIC;
            mcb3_dram_udqs_n  : inout STD_LOGIC;
            mcb3_rzq          : inout STD_LOGIC;
            mcb3_dram_udm     : out STD_LOGIC;
            mcb3_dram_dqs     : inout STD_LOGIC;
            mcb3_dram_dqs_n   : inout STD_LOGIC;
            mcb3_dram_ck      : out STD_LOGIC;
            mcb3_dram_ck_n    : out STD_LOGIC;
            -- ui common
            c3_sys_clk_p  : in STD_LOGIC;  -- 系统参考时钟
            c3_sys_clk_n  : in STD_LOGIC;  --
            c3_sys_rst_i  : in STD_LOGIC;  -- MIG复位信号
            c3_calib_done : out STD_LOGIC; -- MIG初始化完成
            c3_clk0       : out STD_LOGIC; -- MIG给用户提供的时钟
            c3_rst0       : out STD_LOGIC; -- MIG给用户提供的复位
            -- port 0
            c3_p0_cmd_clk       : in STD_LOGIC;                                            -- P0通道命令FIFO的时钟接口
            c3_p0_cmd_en        : in STD_LOGIC;                                            -- P0通道命令FIFO的写使能端口
            c3_p0_cmd_instr     : in STD_LOGIC_VECTOR(2 downto 0);                         -- P0通道命令FIFO的写数据，不同的编码代表不同的操作的命令
            c3_p0_cmd_bl        : in STD_LOGIC_VECTOR(5 downto 0);                         -- P0通道每一个命令，数据FIFO突发的长度
            c3_p0_cmd_byte_addr : in STD_LOGIC_VECTOR(29 downto 0);                        -- P0通道命令操作的起始地址，在 c3_p0_cmd_en 有效的时候被锁存
            c3_p0_cmd_empty     : out STD_LOGIC;                                           -- P0通道命令FIFO的空标志
            c3_p0_cmd_full      : out STD_LOGIC;                                           -- P0通道命令FIFO的满标志
            c3_p0_wr_clk        : in STD_LOGIC;                                            -- P0通道数据写FIFO的时钟
            c3_p0_wr_en         : in STD_LOGIC;                                            -- P0通道数据写FIFO的使能信号
            c3_p0_wr_mask       : in STD_LOGIC_VECTOR(C3_P0_MASK_SIZE - 1 downto 0);       -- P0通道数据写FIFO的数据掩码
            c3_p0_wr_data       : in STD_LOGIC_VECTOR(C3_P0_DATA_PORT_SIZE - 1 downto 0);  -- P0通道数据写FIFO的数据
            c3_p0_wr_full       : out STD_LOGIC;                                           -- P0通道数据写FIFO的满信号
            c3_p0_wr_empty      : out STD_LOGIC;                                           -- P0通道数据写FIFO的空信号
            c3_p0_wr_count      : out STD_LOGIC_VECTOR(6 downto 0);                        -- P0通道数据写FIFO写数据计数信号
            c3_p0_wr_underrun   : out STD_LOGIC;                                           -- 高电平表示写数据FIFO中没有足够的空间供写入数据
            c3_p0_wr_error      : out STD_LOGIC;                                           -- 这个信号表明写入数据FIFO错误发生了，因为FIFO指针没有同步。需要MCB复位才能从这种情况中恢复
            c3_p0_rd_clk        : in STD_LOGIC;                                            -- P0通道读数据FIFO的时钟接口
            c3_p0_rd_en         : in STD_LOGIC;                                            -- P0通道数据读FIFO的使能信号
            c3_p0_rd_data       : out STD_LOGIC_VECTOR(C3_P0_DATA_PORT_SIZE - 1 downto 0); -- P0通道数据读FIFO的数据
            c3_p0_rd_full       : out STD_LOGIC;                                           -- P0通道数据读FIFO的满信号
            c3_p0_rd_empty      : out STD_LOGIC;                                           -- P0通道数据读FIFO的空信号
            c3_p0_rd_count      : out STD_LOGIC_VECTOR(6 downto 0);                        -- P0通道数据读FIFO读数据计数信号
            c3_p0_rd_overflow   : out STD_LOGIC;                                           -- 高电平表示读数据FIFO中没有足够的空间供写入数据
            c3_p0_rd_error      : out STD_LOGIC;                                           -- 这个信号表明读出数据FIFO错误发生了，因为FIFO指针没有同步。需要MCB复位才能从这种情况中恢复
            --port 1
            c3_p1_cmd_clk       : in STD_LOGIC;
            c3_p1_cmd_en        : in STD_LOGIC;
            c3_p1_cmd_instr     : in STD_LOGIC_VECTOR(2 downto 0);
            c3_p1_cmd_bl        : in STD_LOGIC_VECTOR(5 downto 0);
            c3_p1_cmd_byte_addr : in STD_LOGIC_VECTOR(29 downto 0);
            c3_p1_cmd_empty     : out STD_LOGIC;
            c3_p1_cmd_full      : out STD_LOGIC;
            c3_p1_wr_clk        : in STD_LOGIC;
            c3_p1_wr_en         : in STD_LOGIC;
            c3_p1_wr_mask       : in STD_LOGIC_VECTOR(C3_P1_MASK_SIZE - 1 downto 0);
            c3_p1_wr_data       : in STD_LOGIC_VECTOR(C3_P1_DATA_PORT_SIZE - 1 downto 0);
            c3_p1_wr_full       : out STD_LOGIC;
            c3_p1_wr_empty      : out STD_LOGIC;
            c3_p1_wr_count      : out STD_LOGIC_VECTOR(6 downto 0);
            c3_p1_wr_underrun   : out STD_LOGIC;
            c3_p1_wr_error      : out STD_LOGIC;
            c3_p1_rd_clk        : in STD_LOGIC;
            c3_p1_rd_en         : in STD_LOGIC;
            c3_p1_rd_data       : out STD_LOGIC_VECTOR(C3_P1_DATA_PORT_SIZE - 1 downto 0);
            c3_p1_rd_full       : out STD_LOGIC;
            c3_p1_rd_empty      : out STD_LOGIC;
            c3_p1_rd_count      : out STD_LOGIC_VECTOR(6 downto 0);
            c3_p1_rd_overflow   : out STD_LOGIC;
            c3_p1_rd_error      : out STD_LOGIC
        );
    end component;

```