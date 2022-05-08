# FX3

CyU3PIoMatrixConfig_t 作用I2C 总线总是启用，因此io_cfg.useI2C实际上没有意义。

当GPIF工作在 32位模式时，只有SPI/UART/I2S中的其中一个可以工作

此时必须指定io_cfg.lppMode 为 CY_U3P_IO_MATRIX_LPP_DEFAULT

设置 io_cfg.useUART/useI2S/useSPI 中的其中一个为CyTrue其他为CyFalse

————————————————

https://community.infineon.com/t5/USB-superspeed-peripherals/IO-matrix-configuration-problems-in-AN84868/m-p/233608