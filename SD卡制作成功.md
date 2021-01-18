u-boot.32 这个文件必须要


lilei@raylee:~$ umount /dev/sdb1 
lilei@raylee:~$ umount /dev/sdb2
lilei@raylee:~$ cat /proc/partitions 
major minor  #blocks  name

   8        0  234431064 sda
   8        1   97860105 sda1
   8        2     625664 sda2
   8        3          1 sda3
   8        5    7999488 sda5
   8        6     999424 sda6
   8        7   49998848 sda7
   8        8   76941312 sda8
   8       16   61736960 sdb
   8       17     261120 sdb1
   8       18   61474816 sdb2
lilei@raylee:~$ sudo fdisk /dev/sdb
[sudo] lilei 的密码： 

Welcome to fdisk (util-linux 2.27.1).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.


命令(输入 m 获取帮助)： d
分区号 (1,2, default 2): 1

Partition 1 has been deleted.

命令(输入 m 获取帮助)： d
Selected partition 2
Partition 2 has been deleted.

命令(输入 m 获取帮助)： 2
2: unknown command

命令(输入 m 获取帮助)： n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p): p
分区号 (1-4, default 1): 1
First sector (2048-123473919, default 2048): 
Last sector, +sectors or +size{K,M,G,T,P} (2048-123473919, default 123473919): +255M

Created a new partition 1 of type 'Linux' and of size 255 MiB.

命令(输入 m 获取帮助)： n
Partition type
   p   primary (1 primary, 0 extended, 3 free)
   e   extended (container for logical partitions)
Select (default p): p
分区号 (2-4, default 2): 2
First sector (524288-123473919, default 524288): 
Last sector, +sectors or +size{K,M,G,T,P} (524288-123473919, default 123473919): 

Created a new partition 2 of type 'Linux' and of size 58.6 GiB.

命令(输入 m 获取帮助)： t
分区号 (1,2, default 2): 1
Partition type (type L to list all types): c

Changed type of partition 'Linux' to 'W95 FAT32 (LBA)'.

命令(输入 m 获取帮助)： t
分区号 (1,2, default 2): 2
Partition type (type L to list all types): 83

Changed type of partition 'Linux' to 'Linux'.

命令(输入 m 获取帮助)： w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.

lilei@raylee:~$ sudo mkfs.vfat -n boot /dev/sdb1
mkfs.fat 3.0.28 (2015-05-16)
mkfs.fat: warning - lowercase labels might not work properly with DOS or Windows
lilei@raylee:~$ sudo mkfs.ext3 -L rootfs /dev/sdb2
mke2fs 1.42.13 (17-May-2015)
/dev/sdb2 contains a ext3 file system labelled 'rootfs'
	last mounted on /media/lilei/rootfs on Thu Jan 14 12:05:52 2021
无论如何也要继续? (y,n) y
Creating filesystem with 15368192 4k blocks and 3849552 inodes
Filesystem UUID: 35d0831d-3069-4801-9a32-0d43fe97dbae
Superblock backups stored on blocks: 
	32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 
	4096000, 7962624, 11239424

Allocating group tables: 完成                            
正在写入inode表: 完成                            
Creating journal (32768 blocks): 完成
Writing superblocks and filesystem accounting information:        
完成

lilei@raylee:~$ 
lilei@raylee:~$ cd  software/SD/19red/boot/
lilei@raylee:~/software/SD/19red/boot$ ls
BOOTEX.LOG  cse.bin  Image  s32v234-evb.dtb  System Volume Information
lilei@raylee:~/software/SD/19red/boot$ sudo dd if=u-boot.s32 of=/dev/sdb bs=512 seek=8 conv=fsync
dd: 打开'u-boot.s32' 失败: 没有那个文件或目录
lilei@raylee:~/software/SD/19red/boot$ cd ..
lilei@raylee:~/software/SD/19red$ cd ..
lilei@raylee:~/software/SD$ cd ..cd
bash: cd: ..cd: 没有那个文件或目录
lilei@raylee:~/software/SD$ cd ..
lilei@raylee:~/software$ cd ..
lilei@raylee:~$ cd nxp/
lilei@raylee:~/nxp$ ls
kernel  u-boot  WPI_isp_ov10635_single_view  调式成功案例
lilei@raylee:~/nxp$ cd u-boot/
lilei@raylee:~/nxp/u-boot$ sudo dd if=u-boot.s32 of=/dev/sdb bs=512 seek=8 conv=fsync
记录了600+0 的读入
记录了600+0 的写出
307200 bytes (307 kB, 300 KiB) copied, 0.0836294 s, 3.7 MB/s
lilei@raylee:~/nxp/u-boot$ cd ..c
bash: cd: ..c: 没有那个文件或目录
lilei@raylee:~/nxp/u-boot$ cd ..
lilei@raylee:~/nxp$ cd ..
lilei@raylee:~$ cd software/
lilei@raylee:~/software$ cd SD/
lilei@raylee:~/software/SD$ cd 19red/
lilei@raylee:~/software/SD/19red$ cd boot/
lilei@raylee:~/software/SD/19red/boot$ sudo cp Image /media/lilei/boot/
lilei@raylee:~/software/SD/19red/boot$ sudo cp s32v234-evb.dtb /media/lilei/boot/
lilei@raylee:~/software/SD/19red/boot$ sudo cp cse.bin /media/lilei/boot/lilei@raylee:~/software/SD/19red/boot$ sudo cp BOOTEX.LOG /media/lilei/boot/
lilei@raylee:~/software/SD/19red/boot$ cd ..
lilei@raylee:~/software/SD/19red$ cd rootfs/
lilei@raylee:~/software/SD/19red/rootfs$ sudo cp -r ./* /media/lilei/rootfs
lilei@raylee:~/software/SD/19red/rootfs$ sync


















lilei@raylee:~$ sudo fdisk -l
[sudo] lilei 的密码： 
Disk /dev/sda: 223.6 GiB, 240057409536 bytes, 468862128 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x12976705

设备       启动     Start    末尾    扇区   Size Id 类型
/dev/sda1  *         2048 195722257 195720210  93.3G  7 HPFS/NTFS/exFAT
/dev/sda2       195723264 196974591   1251328   611M 27 Hidden NTFS WinRE
/dev/sda3       196976638 468860927 271884290 129.7G  5 扩展
/dev/sda5       196976640 212975615  15998976   7.6G 82 Linux 交换 / Solaris
/dev/sda6       212977664 214976511   1998848   976M 83 Linux
/dev/sda7       214978560 314976255  99997696  47.7G 83 Linux
/dev/sda8       314978304 468860927 153882624  73.4G 83 Linux


Disk /dev/sdb: 58.9 GiB, 63218647040 bytes, 123473920 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xc21f5ba2

设备       启动  Start    末尾    扇区  Size Id 类型
/dev/sdb1         2048    524287    522240  255M  c W95 FAT32 (LBA)
/dev/sdb2       524288 123473919 122949632 58.6G 83 Linux


Disk /dev/sdc: 465.8 GiB, 500107862016 bytes, 976773168 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0x2d4a10ed

设备       启动 Start    末尾    扇区   Size Id 类型
/dev/sdc1        2048 976769023 976766976 465.8G  7 HPFS/NTFS/exFAT
lilei@raylee:~$ umount /dev/sdb1 
lilei@raylee:~$ umount /dev/sdb2
lilei@raylee:~$ cat /proc/partitions 
major minor  #blocks  name

   8        0  234431064 sda
   8        1   97860105 sda1
   8        2     625664 sda2
   8        3          1 sda3
   8        5    7999488 sda5
   8        6     999424 sda6
   8        7   49998848 sda7
   8        8   76941312 sda8
   8       16   61736960 sdb
   8       17     261120 sdb1
   8       18   61474816 sdb2
   8       32  488386584 sdc
   8       33  488383488 sdc1
lilei@raylee:~$ sudo fdisk /dev/sdb

Welcome to fdisk (util-linux 2.27.1).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.


命令(输入 m 获取帮助)： d
分区号 (1,2, default 2): 1

Partition 1 has been deleted.

命令(输入 m 获取帮助)： d
Selected partition 2
Partition 2 has been deleted.

命令(输入 m 获取帮助)： 2
2: unknown command

命令(输入 m 获取帮助)： n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p): p
分区号 (1-4, default 1): 1
First sector (2048-123473919, default 2048): 
Last sector, +sectors or +size{K,M,G,T,P} (2048-123473919, default 123473919): +255M

Created a new partition 1 of type 'Linux' and of size 255 MiB.

命令(输入 m 获取帮助)： n
Partition type
   p   primary (1 primary, 0 extended, 3 free)
   e   extended (container for logical partitions)
Select (default p): p
分区号 (2-4, default 2): 2
First sector (524288-123473919, default 524288): 
Last sector, +sectors or +size{K,M,G,T,P} (524288-123473919, default 123473919): 

Created a new partition 2 of type 'Linux' and of size 58.6 GiB.

命令(输入 m 获取帮助)： t
分区号 (1,2, default 2): 1
Partition type (type L to list all types): c

Changed type of partition 'Linux' to 'W95 FAT32 (LBA)'.

命令(输入 m 获取帮助)： t
分区号 (1,2, default 2): 2
Partition type (type L to list all types): 83

Changed type of partition 'Linux' to 'Linux'.

命令(输入 m 获取帮助)： w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.

lilei@raylee:~$ sudo mkfs.vfat -n boot /dev/sdb1
mkfs.fat 3.0.28 (2015-05-16)
mkfs.fat: warning - lowercase labels might not work properly with DOS or Windows
lilei@raylee:~$ sudo mkfs.ext3 -L rootfs /dev/sdb2
mke2fs 1.42.13 (17-May-2015)
/dev/sdb2 contains a ext3 file system labelled 'rootfs'
	last mounted on /media/lilei/rootfs on Thu Jan 14 13:01:51 2021
无论如何也要继续? (y,n) y
Creating filesystem with 15368192 4k blocks and 3849552 inodes
Filesystem UUID: 6556b084-d2de-47ea-948f-b0c58a6f66d8
Superblock backups stored on blocks: 
	32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 
	4096000, 7962624, 11239424

Allocating group tables: 完成                            
正在写入inode表: 完成                            
Creating journal (32768 blocks): 完成
Writing superblocks and filesystem accounting information: 完成   


lilei@raylee:~$ cd nxp/
lilei@raylee:~/nxp$ cd u-boot/
lilei@raylee:~/nxp/u-boot$ sudo dd if=u-boot.s32 of=/dev/sdb bs=512 seek=8 conv=fsync
记录了600+0 的读入
记录了600+0 的写出
307200 bytes (307 kB, 300 KiB) copied, 0.0698745 s, 4.4 MB/s
lilei@raylee:~/nxp/u-boot$ cd ~
lilei@raylee:~$ cd /media/
lilei@raylee:/media$ cd lilei/
lilei@raylee:/media/lilei$ ls
boot  lilei  rootfs
lilei@raylee:/media/lilei$ cd lilei/
lilei@raylee:/media/lilei/lilei$ cd 科研
lilei@raylee:/media/lilei/lilei/科研$ ls
ADAS     PPT      ubuntu_File_最新  大联大    雷达            中期答辩
C++      Python   Ubuntu 深度学习   公司      内江毫米波项目  自写文档
dataset  S32V     video             公司git   人工智能
ML       SD 最新  vm_adas_hog_data  基地实践  碎片记录
OpenCV   Ubuntu   毕业论文撰写      开题      下载资料
lilei@raylee:/media/lilei/lilei/科研$ cd SD\ 最新/
lilei@raylee:/media/lilei/lilei/科研/SD 最新$ ls
boot  rootfs
lilei@raylee:/media/lilei/lilei/科研/SD 最新$ cd boot/
lilei@raylee:/media/lilei/lilei/科研/SD 最新/boot$ ls
BOOTEX.LOG  cse.bin  Image  s32v234-evb.dtb  System Volume Information
lilei@raylee:/media/lilei/lilei/科研/SD 最新/boot$ 
lilei@raylee:/media/lilei/lilei/科研/SD 最新/boot$ 
lilei@raylee:/media/lilei/lilei/科研/SD 最新/boot$ 
lilei@raylee:/media/lilei/lilei/科研/SD 最新/boot$ 
lilei@raylee:/media/lilei/lilei/科研/SD 最新/boot$ sudo cp Image /media/lilei/boot/
lilei@raylee:/media/lilei/lilei/科研/SD 最新/boot$ sudo cp s32v234-evb.dtb /media/lilei/boot/
lilei@raylee:/media/lilei/lilei/科研/SD 最新/boot$ sudo cp cse.bin /media/lilei/boot/
lilei@raylee:/media/lilei/lilei/科研/SD 最新/boot$ sudo cp BOOTEX.LOG /media/lilei/boot/
lilei@raylee:/media/lilei/lilei/科研/SD 最新/boot$ cd ..
lilei@raylee:/media/lilei/lilei/科研/SD 最新$ cd rootfs/
lilei@raylee:/media/lilei/lilei/科研/SD 最新/rootfs$ sudo cp -r ./* /media/lilei/rootfs
cp: 无法访问'./home/root/demo/data/common/dev/disk/by-path': 输入/输出错误
cp: 无法访问'./home/root/demo/data/common/dev/disk/by-uuid': 输入/输出错误


cp: 读取'./home/root/demo/data/common/etc/sane.d/dll.conf' 时出错: 输入/输出错误
cp: 读取'./opt/gpu_demos/test/sdk/samples/vdk/es20/samples/sample9/android/src/com/vivantecorp/graphics/sample9/GL2Sample9Activity.java' 时出错: 输入/输出错误


cp: 无法访问'./usr/share/common-licenses/fixesproto-dev': 输入/输出错误


lilei@raylee:/media/lilei/lilei/科研/SD 最新/rootfs$ 
lilei@raylee:/media/lilei/lilei/科研/SD 最新/rootfs$ 
lilei@raylee:/media/lilei/lilei/科研/SD 最新/rootfs$ 
lilei@raylee:/media/lilei/lilei/科研/SD 最新/rootfs$ 
lilei@raylee:/media/lilei/lilei/科研/SD 最新/rootfs$ 
lilei@raylee:/media/lilei/lilei/科研/SD 最新/rootfs$ 
lilei@raylee:/media/lilei/lilei/科研/SD 最新/rootfs$ sync


