# makefile

make 规则中的每行命令是在一个单独的 shell 中执行的， 这和 shellscript 不同，做一个简单测试：

```makefile
source:
        pwd
        cd /tmp
        pwd
```

可以看到 cd 后，当前的目录并没有改变。

## 格式 

```
<target>: [prerequisites]
<tab> [commands]
```

总之，make 的规则就是 目标 target 由 前置条件 prerequisites 组成，更新 target 的步骤是 commands。

makefile 只对变动的文件重新构建，虽然 shellscript 也能做到这一点（如 nginx），但比较麻烦。

有些规则不需要去检测文件是否变动（对比文件时间戳），可以用伪目标 phony target，如 `.PHONY: clean`。

makefile 会按照目标依赖顺序执行规则，如果没有指定，那就是从第一个命令开始。

## 语法

- `#` 注释
- `@` 关闭执行步骤提示 （位于 commands 前面）
- `wildcard` 跟 bash 一致的通配符
- `$(variable)` 类 bash 变量，= 两边可以空格，用() 而不是 {}
- `$$shell_varuable` 这点确实不知道，makefile 会对 $ 转义，所以需要重复。

makefile 支持变量，关于赋值语句，有下面的区分

```makefile
VARIABLE ?= value # 只有在该变量为空时才设置值。

VARIABLE += value # 将值追加到变量的尾端。

VARIABLE = value  # 在运行时扩展，允许递归扩展，适合变量。

VARIABLE := value # 在定义时扩展，适合常量。
```

- `$(CC)` 当前编译器
- `$(MAKE)` 当前 make 命令
- `$@` 当前指定的 target 
- `$<` target 的第一个前置条件
- `$?` 比 target 时间戳新的 所有前置条件
- `$^` 所有前置条件
- `$*` 匹配符 % 指代的部分
- `$(@D)` $@ 的目录名
- `$(@F)` $@ 的文件名
- `$(<D)` $< 的目录名
- `$(<F)` $< 的文件名


逻辑分支、循环和函数就不展开了，至今很少遇见过使用的例子，频率太低。（大型项目一般上 cmake）

## 参考

- https://www.ruanyifeng.com/blog/2015/02/make.html
- https://www.cnblogs.com/tp-16b/p/8955462.html


