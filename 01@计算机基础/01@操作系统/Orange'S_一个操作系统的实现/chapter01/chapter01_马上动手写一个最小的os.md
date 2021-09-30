# chapter01 马上动手写一个最小的OS

## 1.1 准备工作

1. 安装虚拟机
2. 安装ubuntu操作系统
3. 安装nasm



## 1.2 十分钟完成的操作系统

```asm
;The first program for os
org 07c00h
mov ax, cs
mov ds, ax
mov es, ax
call puts
jmp $

puts:
	mov ax, BootMessage
	mov bp, ax
	mov cx, 16
	mov ax, 01301h
	mov bx, 000ch
	mov dl, 0
	int 10h
	ret
BootMessage: db "Hello World!"
times 510 - ($ - $$) db 0
dw 0xaa55
```

