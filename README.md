# xilinx_microblaze_upgrade_fpga
FPGA软核远程升级设计

1.	简介及硬件环境
FPGA软核远程升级设计，使用串口助手升级，无需通信协议，支持921600bps。

环境：xc7a200tfbg484+N25Q128。

用到的IP核有：

MicroBlaze(v11.0)

MIG 7Series(v4.2)

AXI UART16550(v2.0)

AXI Quad SPI(v3.2)

AXI Interrupt Controller(v4.4) 

AXI HWICAP(v3.0)

3.	设计说明
 
(1)程序运行后，等待接收升级指令

(2)接收帧头EB, 90, 0A, 01

(3)接收烧写地址，烧写长度，指令校验

(4)接收长度LEN字节升级数据

(5)启动FLASH烧写

(6)启动FLASH回读校验

(7)如果通过，启动IPROG内部复位；

如果失败，重启进备份镜像重新远程升级。

3.	升级文件格式

偏移	0-3             4-7             8-11            12-15           16-N

数据	EB 90 0A 01     烧写地址        烧写长度         指令字段校验     FPGA BIN文件

 

