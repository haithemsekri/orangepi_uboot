# orangepi_uboot

Precompiled u-boot binaries for 32bit ARM Orange PI boards, optimized for small size.

Build "machine"
Kernel version : Linux archOrangePiPC 4.17.6-1-ARCH #1 SMP PREEMPT Fri Jul 13 00:41:20 UTC 2018 armv7l GNU/Linux
GCC options: CFLAGS="-march=armv7-a -mfloat-abi=hard -mfpu=vfpv3-d16 -Os -pipe -fstack-protector-strong -fno-plt"
GCC version: gcc (GCC) 8.1.1 20180531

201807 release tested on:
Orange PI PC
Orange PI Plus 2e

201811 release tested on :
Orange PI PC

Steps to rebuild (on native ARMv7 machine):
wget ftp://ftp.denx.de/pub/u-boot/u-boot-2018.11.tar.bz2
tar -jxf u-boot-2018.11.tar.bz2
virtualenv -p /usr/bin/python2.7 my_uboot
source my_uboot/bin/activate
make -j5 orangepi_pc_defconfig
make -j5
