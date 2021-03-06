[TOC]

# chapter06_文件系统管理

## 8.1 查看磁盘或者目录的容量

### 8.1.1 df命令

命令`df`（disk filesystem的简写）用于查看已挂载磁盘的总容量、使用容量、剩余容量等，其后可以不加任何参数，显示数据默认以KB为单位

命令语法：`df [参数] [目录或文件名]`

参数说明：

参数	说明
-a	列出所有的文件系统，包括系统特有的/proc等文件系统。
-k	以KBytes为单位，返回各文件系统容量。
-m	以MBytes为单位，返回各文件系统容量。
-h	以GBytes、MBytes、KBytes为单位，以合适的单位，返回各文件系统容量。
-H	以M=1000K取代M=1024K的进位方式显示各文件系统容量。
-T	显示文件系统类型。
-i	显示inode信息。
使用示例：

1. df基本命令

```shell
# df

```

2. 查看inode使用状况，如果已经使用100%，那么即使磁盘空间有剩余，也会提示磁盘空间已满

```shell
# df -i | grep -v tmpfs

```

3. 显示系统内的所有特殊文件格式、名称及磁盘使用情况

```shell
# df -aT
```

### 8.1.2 du命令

命令`du`（disk useage）用来查看某个目录或文件所占空间的大小，其格式为`du [-abckmsh] [文件或者目录名]`

参数说明：

| 参数 | 说明                        |
| ---- | --------------------------- |
| -a   | 列出所有的文件与目录容量。  |
| -h   | 以G、M、K为单位，返回容量。 |
| -s   | 列出总量。                  |
| -S   | 列出不包括子目录下的总量。  |
| -k   | 以KBytes为单位，返回容量。  |
| -m   | 以MBytes为单位，返回容量。  |

`du -sh file`可以查看一个文件或目录的磁盘占用情况。-s显示总用量，如果查看目录时不加-s则显示目录下各个文件的情况。-h以合适单位显示大小。

文件大小还可以在`ls -l`中看到。但是与du命令不同，ls显示的是实际文件大小，du显示的是占用磁盘大小。其实挺好理解，前面说磁盘格式化就像在白纸上画格子，那么每个格子（block）就会有一定大小来存储内容。一个格子（block）不能放多个文件的内容，不然会造成混乱。也就是说文件即使占用半个block大小，这个block不再被别的文件使用。du就是从block大小来衡量文件大小的，而ls是从文件存放bit信息量来衡量。当然du也可以查看文件内容大小，需要使用参数-sb。

## 8.2 磁盘的分区和格式化

### 8.2.1 增加虚拟磁盘

vmware添加虚拟磁盘

### 8.2.2 fdisk命令

`fdisk`是Linux下硬盘的分区工具，是一个非常实用的命令，但是此命令只能划分小于2TB的分区。该命令的格式为`fdisk [-l ] [设备名称]`，其选项只有`-l`。选项`-l`后面如果不加设备名称，就会直接列出系统中所有的磁盘设备以及分区表；如果加上设备名称，则会列出该设备的分区表

https://blog.csdn.net/IHBOS/article/details/113267785?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165317934416780357235255%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=165317934416780357235255&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-22-113267785-null-null.142^v10^control,157^v4^control&utm_term=%E7%A3%81%E7%9B%98%E7%AE%A1%E7%90%86&spm=1018.2226.3001.4187