# 【RuyiSDK VS Code 扩展】Linux 篇 06：准备一个方便调试的 C 示例

> 状态：示例代码与 Makefile 已加入仓库
>
> 实测版本：GNU Make、`riscv64-unknown-linux-gnu-gcc`
>
> 本篇标签：`RuyiSDK`、`Linux`、`VS Code`、`RISC-V`、`C`、`上手记录`

仓库已经提供 `examples/hello-ruyi`。这个示例比只有一行 `printf` 稍多一点：它保留函数参数和局部变量，后面可以在 GDB 中观察 `a`、`b`、`result` 和 `value`。

## 目录结构

```text
examples/hello-ruyi/
├── .vscode/
│   └── launch.json
├── Makefile
├── README.md
└── hello.c
```

在 IDE 中使用“文件 → 打开文件夹”，把 `examples/hello-ruyi` 作为工作区根目录打开。Build 功能只会从工作区根目录检测构建标志文件。

![示例项目目录树](./assets/images/06-01-project-tree.png)

![示例项目目录树的放大截图](./assets/images/06-01-project-tree-zoom.png)

## hello.c

```c
#include <stdio.h>

static int add(int a, int b)
{
    int result = a + b;
    return result;
}

int main(void)
{
    int value = add(20, 22);
    printf("Hello RISC-V, value=%d\n", value);
    return value == 42 ? 0 : 1;
}
```

程序正常输出：

```text
Hello RISC-V, value=42
```


## Makefile

```make
TARGET := hello-riscv
CC := riscv64-unknown-linux-gnu-gcc
CFLAGS := -g -O0 -Wall -Wextra
LDFLAGS := -static

.PHONY: all clean

all: $(TARGET)

$(TARGET): hello.c
	$(CC) $(CFLAGS) $< -o $@ $(LDFLAGS)

clean:
	rm -f $(TARGET)
```

几个参数的作用：

- `-g`：写入源码级调试信息。
- `-O0`：关闭优化，让变量和单步行为更容易观察。
- `-Wall -Wextra`：打开常用警告。
- `-static`：静态链接，QEMU user mode 不必另外寻找 Target 动态链接器。


```bash
make CC=/另一套工具链/bin/riscv64-unknown-linux-gnu-gcc
```

![hello.c 和 Makefile](./assets/images/06-02-source-and-makefile.png)

![hello.c 和 Makefile 的放大截图](./assets/images/06-02-source-and-makefile-zoom.png)


上一篇：[安装 GNU 工具链、QEMU 和基础工具](05-toolchain-qemu.md)  
下一篇：[创建并激活 Ruyi 虚拟环境](07-ruyi-venv.md)
