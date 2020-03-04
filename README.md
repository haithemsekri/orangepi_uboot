# orangepi_uboot
  
Precompiled u-boot binaries for all 32bit and 64bit Allwinner based Orange PI boards, optimized for small size. DTB (device tree blob) included from release 201907!

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

### 201907 release (Cross-compile)
  Build machine Kernel version: Arch Linux archBalazsPC 5.2.10-1-ck #1 SMP PREEMPT Wed Sep 4 14:09:32 CEST 2019 x86_64 GNU/Linux
  GCC options: CFLAGS="-march=armv7-a -mfloat-abi=hard -mfpu=vfpv3-d16 -Os -pipe -fstack-protector-strong -fno-plt"  
  GCC version: gcc version 9.1.0 (Arch Repository)  
  tested on :  
  Orange PI Zero (Xradio wifi works with https://aur.archlinux.org/packages/xradio-git alongside the dtb file!)  

### 202001 release (Cross-compile)
  Build machine Kernel version: Linux archBalazsPC 5.5.3-1-ck-zen #1 SMP PREEMPT Tue, 11 Feb 2020 23:04:25 +0000 x86_64 GNU/Linux
  GCC options: CFLAGS="-march=armv7-a -mfloat-abi=hard -mfpu=vfpv3-d16 -Os -pipe -fstack-protector-strong -fno-plt"  
  GCC options: CFLAGS="-march=armv8-a -march=armv8-a -Os -pipe -fstack-protector-strong -fno-plt" 
  GCC version: gcc version 9.2.0 (Arch Repository)  
  tested on :  
  Orange PI PC
  Orange PI Zero Plus

Steps to rebuild (OPI PC || 32bit Allwinner H3):
```bash
wget ftp://ftp.denx.de/pub/u-boot/u-boot-2020.01.tar.bz2
tar -xf u-boot-2020.01.tar.bz2
cd u-boot-2020.01
virtualenv -p /usr/bin/python2.7 my_uboot
source my_uboot/bin/activate
make orangepi_pc_defconfig
make ARCH=arm MARCH=armv7 CFLAGS="-march=armv7-a -mfloat-abi=hard -mfpu=vfpv3-d16 -Os -pipe -fstack-protector-strong -fno-plt" CROSS_COMPILE=/usr/bin/arm-none-eabi- -j4
dd if=orangepi_pc/u-boot-sunxi-with-spl.bin of=/dev/sdX bs=1024 seek=8
```

Steps to rebuild (OPI Z+ || 64 bit Allwinner H5):
```bash
git clone https://github.com/ARM-software/arm-trusted-firmware.git
cd arm-trusted-firmware
git checkout v2.2
make CROSS_COMPILE=aarch64-linux-gnu- PLAT=sun50i_a64 DEBUG=1 -j4 bl31
wget ftp://ftp.denx.de/pub/u-boot/u-boot-2020.01.tar.bz2
tar -xf u-boot-202-.01.tar.bz2
cd u-boot-2020.01
cp ${arm-trusted-firmware_dir}/build/sun50i_a64/debug/bl31.bin .
virtualenv -p /usr/bin/python2.7 my_uboot
source my_uboot/bin/activate
make orangepi_zero_plus_defconfig
make ARCH=arm MARCH=armv8a CFLAGS="-march=armv8-a -march=armv8-a -Os -pipe -fstack-protector-strong -fno-plt" CROSS_COMPILE=/usr/bin/aarch64-linux-gnu- -j4
dd if=orangepi_zero_plus/u-boot-sunxi-with-spl.bin of=/dev/sdX bs=8k seek=1
```

### Size comparison across releases
|             | 201807 | 201811 | 201904 | 201907 | 202001 |
|-------------|--------|--------|--------|--------|--------|
| OrangePI PC | 361K   | 413K   | 459K   | 470K   | 467K   |
