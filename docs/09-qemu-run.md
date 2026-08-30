# 【RuyiSDK VS Code 扩展】Linux 篇 09：用 QEMU 运行程序


> 本篇标签：`RuyiSDK`、`Linux`、`VS Code`、`RISC-V`、`QEMU`、`上手记录`

本篇按 x86_64 Host 演示。创建 venv 时如果已经加入 Ruyi QEMU，后面直接使用 \ruyi-qemu`。`

先确认 Host 架构和 ELF：

```bash
uname -m
file ./hello-riscv
```

x86_64 路线：

```bash
command -v ruyi-qemu
ruyi-qemu --version
```

![x86_64 Host 的 QEMU 运行命令](./assets/images/09-01-runtime-choice.png)

![x86_64 Host 的 QEMU 运行命令放大截图](./assets/images/09-01-runtime-choice-zoom.png)

## 运行静态 ELF

x86_64 + Ruyi QEMU：

```bash
ruyi-qemu ./hello-riscv
echo $?
```

预期：

```text
Hello RISC-V, value=42
0
```

![QEMU 运行结果](./assets/images/09-02-qemu-run.png)

![QEMU 运行结果的放大截图](./assets/images/09-02-qemu-run-zoom.png)


上一篇：[交叉编译并检查 RISC-V ELF](08-build-and-elf.md)  
下一篇：[用 QEMU 和 GDB 调试程序](10-qemu-gdb.md)
