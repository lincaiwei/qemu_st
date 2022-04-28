# 编译&执行



## 编译环境依赖：

在全新安装 Ubuntu 20.04 时，以下命令将安装依赖项：

```
sudo apt-get install build-essential python zlib1g-dev libglib2.0-dev libpixman-1-dev libtool libfdt-dev
```



## 典型构建的命令：

```
./configure --enable-debug --disable-werror --target-list="arm-softmmu" 
make
```





## 编译选项：

比如：

```
我们将以下选项传递给“configure”命令以忽略警告（否则警告将导致构建失败）：
    --disable-werror
即
./configure --enable-debug --disable-werror --target-list="arm-softmmu" 
make
```



控制 STM32 实现的其他配置选项：

```
 --extra-cflags=-DDEBUG_CLKTREE
        打印出时钟树调试语句。

    --extra-cflags=-DDEBUG_STM32_RCC 
    --extra-cflags=-DDEBUG_STM32_UART 
    --extra-cflags=-DDEBUG_STM32_TIMER
        打印特定外围设备的调试语句。

    --extra-cflags=-DSTM32_UART_NO_BAUD_DELAY
        禁用波特率时序模拟（即 UART 将尽可能快地发送或接收，而不是使用实际延迟）。

    --extra-cflags=-DSTM32_UART_ENABLE_OVERRUN
    如果在处理最后一个字符之前接收到一个字符，则启用溢出标志的设置。
    如果未设置，UART将不会接收下一个字符，直到前一个字符被软件读取。
    虽然不太现实，但如果 VM运行缓慢，这会更安全。
  
 其他对故障排除有用的 QEMU 配置选项：
    --extra-cflags=-DDEBUG_GIC 
```

比如：

```
./configure --enable-debug --disable-werror --target-list="arm-softmmu" --extra-cflags=-DDEBUG_STM32_UART
make
```









# 执行



执行固件。

```
qemu_stm32-stm32/arm-softmmu/qemu-system-arm -M stm32-p103 -kernel main.bin
```



执行固件的串口内容输出到./tmp/serial.out文件中。

```
qemu_stm32-stm32/arm-softmmu/qemu-system-arm -M stm32-p103 -kernel main.bin -serial file:./tmp/serial.out
```



执行的固件的串口内容输出到stdio中。

```
qemu_stm32-stm32/arm-softmmu/qemu-system-arm -M stm32-p103 -kernel main.bin -serial stdio
```



















































