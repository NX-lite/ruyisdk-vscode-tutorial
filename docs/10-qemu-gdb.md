# 【RuyiSDK VS Code 扩展】Linux 篇 10：用 QEMU 和 GDB 调试程序

> 本篇标签：`RuyiSDK`、`Linux`、`VS Code`、`RISC-V`、`QEMU`、`GDB`、`上手记录`

## 调试前确认

```bash
file ./hello-riscv
command -v riscv64-unknown-linux-gnu-gdb
ss -ltn | grep ':1234'
```

要求：

- EELF 包含调试信息，并且没有被 strip；
- 交叉 GDB 来自当前 venv；
- 端口 1234 没有被其他程序监听。

## 终端 1：启动 QEMU gdbstub

x86_64 + Ruyi QEMU：

```bash
ruyi-qemu -g 1234 ./hello-riscv
```

命令启动后没有立即输出是正常的：程序在等待 GDB 连接。

![QEMU gdbstub 等待连接](./assets/images/10-01-gdbstub.png)

![QEMU gdbstub 等待连接的放大截图](./assets/images/10-01-gdbstub-zoom.png)

## 终端 2：连接交叉 GDB

先确认终端中当前 venv 仍然有效，再执行：

```bash
riscv64-unknown-linux-gnu-gdb ./hello-riscv
```

在 GDB 中依次输入：

```gdb
target remote :1234
break main
break add
continue
next
info args
next
print result
finish
next
print value
continue
quit
```

这组顺序与源码作用域对应：

1. `continue` 先停在 `main`。
2. `next` 执行 `main` 的调用语句；由于 `add` 有断点，会进入 `add`。
3. `info args` 显示 `a = 20`、`b = 22`。
4. 再执行 `next` 完成 `result = a + b`，此时 `print result` 显示 `42`。
5. `finish` 返回 `main`。
6. 再执行一次 `next` 完成对 `value` 的赋值，然后 `print value` 显示 `42`。
7. 最后 `continue` 让程序退出，终端 1 输出 Hello 信息。


![GDB 命中 main 和 add 断点](./assets/images/10-02-gdb-breakpoints.png)

![GDB 断点的放大截图](./assets/images/10-02-gdb-breakpoints-zoom.png)

![GDB 查看 result 和 value](./assets/images/10-03-gdb-variables.png)

![GDB 变量结果的放大截图](./assets/images/10-03-gdb-variables-zoom.png)

初次连接时可能看到 glibc 启动文件 `start.S` 不在本地的提示。只要之后能命中本项目的 `main/add`，它不影响调试。

## VS Code 图形调试

仓库已经提供 `.vscode/launch.json`。它使用 Microsoft C/C++ 扩展的 `cppdbg`，因此这部分针对官方 VS Code。

1. 安装并启用 Microsoft C/C++ 扩展。
2. 确保 venv 路径就是工作区中的 `.ruyi-venv`。
3. 按前面的方式在终端 1 启动 QEMU gdbstub。
4. 在 `hello.c` 的 `add` 函数内设置断点。
5. 打开“运行和调试”，选择“QEMU gdbstub: hello-riscv”。
6. 按 F5 连接，观察 Variables、Call Stack 与 Debug Console。

配置内容：

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "QEMU gdbstub: hello-riscv",
      "type": "cppdbg",
      "request": "launch",
      "program": "${workspaceFolder}/hello-riscv",
      "cwd": "${workspaceFolder}",
      "MIMode": "gdb",
      "miDebuggerPath": "${workspaceFolder}/.ruyi-venv/bin/riscv64-unknown-linux-gnu-gdb",
      "miDebuggerServerAddress": "localhost:1234",
      "stopAtEntry": false,
      "externalConsole": false,
      "setupCommands": [
        {
          "description": "Enable GDB pretty-printing",
          "text": "-enable-pretty-printing",
          "ignoreFailures": true
        }
      ]
    }
  ]
}
```


![VS Code 图形调试](./assets/images/10-04-vscode-debug.png)

![VS Code 图形调试的放大截图](./assets/images/10-04-vscode-debug-zoom.png)



上一篇：[用 QEMU 运行程序](09-qemu-run.md)  
