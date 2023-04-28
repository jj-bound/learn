```toc
```

# 1   adr_l
![[adrl define.png]]
## 1.1   输入
	sym:变量，函数或者标号的地址

## 1.2   输出
	dst:获取到的sym的地址

## 1.3   宏实现
	该宏的主要用处是获取sym的地址并给到dst,首先使用adrp获取到sym所在的页地址，页大小为4KB。然后再执行add将sym基于页的偏移地址加入dst。其中:lo12:就表示获取低12位的数值。

## 1.4   相关汇编指令
adrp:请参考 [[armv8 instruction#1 adrp|adrp]]
add:请参考[[armv8 instruction#^add|add]]
