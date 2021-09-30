安装samba

```shell
apt-get install samba samba-common
smbpasswd -a yanyun
vi /etc/samba/smb.conf
# 添加如下信息
[yanyun]
  browseable = yes 
  path = /home/yanyun/
  available = yes 
  writable = yes 
# mark掉如下
# map to guest = bad user
# 启动：service smbd restart
```

安装bochs

```
apt-get install xorg-dev
apt-get install libgtk2.0-dev

make
出现error:
/usr/bin/ld: gui/libgui.a(gtk_enh_dbg_osdep.o): undefined reference to symbol 'pthread_create@@GLIBC_2.2.5'
//lib/x86_64-linux-gnu/libpthread.so.0: error adding symbols: DSO missing from command line
collect2: error: ld returned 1 exit status
make: *** [bochs] Error 1

修改Makefile:
LIBS =  -lm -lgtk-x11-2.0 -lgdk-x11-2.0 -latk-1.0 -lgio-2.0 -lpangoft2-1.0 -    lpangocairo-1.0 -lgdk_pixbuf-2.0 -lcairo -lpango-1.0 -lfontconfig -lgobject-    2.0 -lglib-2.0 -lfreetype  -lpthread 
添加pthread库

make install
确定bochs的安装路径：
which bochs
/usr/local/bin/bochs

安装 vgabios
apt-get install vgabios
安装路径：
whereis vgabios
vgabios: /usr/share/vgabios

```

```shell
# bochsrc.txt
###############################################################
# Configuration file for Bochs
###############################################################

# how much memory the emulated machine will have
megs: 32

# filename of ROM images
romimage: file=/usr/local/share/bochs/BIOS-bochs-latest
vgaromimage: file=/usr/share/vgabios/vgabios.bin

# what disk images will be used
floppya: 1_44=boot.img, status=inserted

# choose the boot disk.
boot: floppy

# where do we send log messages?
# log: bochsout.txt

# disable the mouse
mouse: enabled=0

# enable key mapping, using US layout as default.
keyboard_mapping: enabled=1, map=/usr/local/share/bochs/keymaps/x11-pc-us.map
```

安装git

```shell
apt-get install git
# 配置：https://www.jianshu.com/p/6e1de95828a8
```

