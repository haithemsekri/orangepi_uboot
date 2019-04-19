# orangepi_uboot
  
Precompiled u-boot binaries for 32bit ARM Orange PI boards, optimized for small size.

### 201807 release (native ARMv7 build)
  Build "machine" Kernel version : Linux archOrangePiPC 4.17.6-1-ARCH #1 SMP PREEMPT Fri Jul 13 00:41:20 UTC 2018 armv7l GNU/Linux  
  GCC options: CFLAGS="-march=armv7-a -mfloat-abi=hard -mfpu=vfpv3-d16 -Os -pipe -fstack-protector-strong -fno-plt"  
  GCC version: gcc (GCC) 8.1.1 20180531  
  tested on:  
  Orange PI PC  
  Orange PI Plus 2e  

### 201811 release (native ARMv7 build)
  Build "machine" Kernel version : Linux archOrangePiPC 4.17.6-1-ARCH #1 SMP PREEMPT Fri Jul 13 00:41:20 UTC 2018 armv7l GNU/Linux  
  GCC options: CFLAGS="-march=armv7-a -mfloat-abi=hard -mfpu=vfpv3-d16 -Os -pipe -fstack-protector-strong -fno-plt"  
  GCC version: gcc (GCC) 8.1.1 20180531  
  tested on :  
  Orange PI PC  

### 201904 release (Cross-compile)
  Build machine Kernel version: Arch Linux 4.19.2-1-ck #1 SMP PREEMPT Thu Jan 3 17:40:34 CET 2019 x86_64 GNU/Linux  
  GCC options: CFLAGS="-march=armv7-a -mfloat-abi=hard -mfpu=vfpv3-d16 -Os -pipe -fstack-protector-strong -fno-plt"  
  GCC version: gcc version 8.3.0 (Arch Repository)  
  tested on :  
  Orange PI PC  

Steps to rebuild:
```bash
wget ftp://ftp.denx.de/pub/u-boot/u-boot-2019.04.tar.bz2
tar -xf u-boot-2019.04.tar.bz2
cd u-boot-2019.04
virtualenv -p /usr/bin/python2.7 my_uboot
source my_uboot/bin/activate
make orangepi_pc_defconfig
make ARCH=arm MARCH=armv7 CFLAGS="-march=armv7-a -mfloat-abi=hard -mfpu=vfpv3-d16 -Os -pipe -fstack-protector-strong -fno-plt" CROSS_COMPILE=/usr/bin/arm-none-eabi- -j4
```

### Size comparison across releases
|  	| 201807 	| 201811 	| 201904 	|
|-------------	|--------	|--------	|--------	|
| OrangePI PC 	| 361K 	| 413K 	| 459K 	|
