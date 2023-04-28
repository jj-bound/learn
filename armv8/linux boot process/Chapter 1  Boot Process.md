```toc
```
# 1   总体启动流程

![[head.S boot flow.svg]]


# 2   启动代码分析
## 2.1   preserve_boot_args

![[preserve_boot_args函数内容.png]]
### 2.1.1   函数功能
	bootloader启动以后会传递4个参数给内核，依次是x0,x1,x2,x3。其中x0是设备树的地址，x1,x2,x3暂时预留。这个函数的功能是将这4个参数放入linux定义好的一个全局变量中，并
将这个全局变量所对应的cache高速缓存清除。

### 2.1.2   代码说明
mov x21，x0  
	x0是bootloader传递的参数，是设备树的地址，这里就是赋值给了x21寄存器
adr_l  x0, boot_args 
	adr_l是linux内核定义的宏，相关实现可以参考[[armv8 asm define description#1 adr_l|adr_l]],boot_args是定义的全局变量，在arch/arm64/kernel/setup.c中定义：
	![[boot_args变量定义.png]]
	这条语句就是将boot_args的地址赋值给x0
stp x21,x1, [x0]
	将x21,x1两个寄存器的值存入boot_args中，x21为设备树的地址，stp汇编指令参考[[armv8 instruction#3 stp|stp]]
	