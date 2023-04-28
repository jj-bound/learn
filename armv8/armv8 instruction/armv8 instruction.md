```toc
```
# 1   add

## 1.1   immediate
![[add immediate instruction.png]]
将寄存器中的值和立即数相加，并赋值给另一个寄存器，使用时需要注意以下几点：
1.寄存器只能是通用寄存器x0-x30,或者sp
2.只能是左移，且左移的大小是固定的12位。或者不移位
3.此汇编指令不会影响到NZCV的状态

## 1.2   register
![[add register.png]]
将两个寄存器的值相加，并赋值给另一个寄存器，使用时需要注意以下几点：
1.寄存器只能是通用寄存器，x0-x30
2.支持lsl,lsr以及asr

# 2   adrp
![[adrp instruction.png]]
这个指令主要是获取到label所在的当前页的基地址。寻址范围为+/-4GB,最高位为符号位，页大小为4KB。这是一个与地址无关的指令，不管当前代码运行在什么地址，他只是通过编译生成时执行adrp的地址与label的偏移量作为immhi,immlo，然后在运行时通过当前PC的地址查找label所在的地址

# 3   stp
![[stp instruction description.png]]

stp:将两个寄存器的值加载到另一个寄存器所指向的地址中，他有3中表现形式：
## 3.1   Post-index
![[stp post-index.png]]
这种是将xt1,xt2的值先放进xn或者sp，然后xn以及sp再加上增量。注意增量如果是aarch32时是必须是4字节对齐的且范围是-256~252，如果是aarch64时必须是8字节对齐，且范围是-512~504，xt1,xt2必须是通用寄存器。

## 3.2   Pre-index
![[stp pre-index.png]]
这种是先将xn或者sp的值加上imm增量，然后将xt1,xt2的值放入。注意增量如果是aarch32时是必须是4字节对齐的且范围是-256~252，如果是aarch64时必须是8字节对齐，且范围是-512~504，xt1,xt2必须是通用寄存器。

## 3.3   signed offset
![[signed offset.png]]
这种和pre index差不多，只不过可以不使用imm增量，注意如果使用增量的话在aarch32时是必须是4字节对齐的且范围是-256~252，在aarch64时必须是8字节对齐，且范围是-512~504，xt1,xt2必须是通用寄存器。