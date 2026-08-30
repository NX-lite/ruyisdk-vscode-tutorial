# 【RuyiSDK VS Code 扩展】Linux 篇 07：创建并激活 Ruyi 虚拟环境

> 本篇标签：`RuyiSDK`、`Linux`、`VS Code`、`RISC-V`、`venv`、`上手记录`


## 创建前确认

在 Packages 中确认：

- `gnu-upstream` 已安装；
- x86_64 Host 若要用 `ruyi-qemu`，`qemu-user-riscv-upstream` 也已安装；
- 当前工作区是 `examples/hello-ruyi`。

## 使用扩展创建

1. 打开 `RuyiSDK 虚拟环境`。
2. 点击工具栏 `+`。
3. Profile 选择 `generic`。
4. 工具链选择已安装的 `gnu-upstream`。
5. sysroot 选择 `Default`，使用工具链随附 sysroot。
6. 如果 Host 是 x86_64，并且已经安装 Ruyi QEMU，模拟器选择`qemu-user-riscv-upstream`；
7. 环境名称填写 `hello-riscv`。
8. 路径选择工作区中的 `.ruyi-venv`。
9. 完成创建。



![Ruyi 虚拟环境创建向导](../assets/07-01-create-venv.png)

![Ruyi 虚拟环境创建向导的放大截图](../assets/07-01-create-venv-zoom.png)

## 激活环境

创建完成后，在列表中点击 `hello-riscv`。底部状态栏应显示当前激活的环境。

然后关闭旧终端，新建一个集成终端。检查：

```bash
command -v riscv64-unknown-linux-gnu-gcc
command -v riscv64-unknown-linux-gnu-gdb
riscv64-unknown-linux-gnu-gcc --version
```

如果是 x86_64，并且创建 venv 时选择了 Ruyi QEMU，再检查：

```bash
command -v ruyi-qemu
ruyi-qemu --version
```

![已激活的 Ruyi 虚拟环境](../assets/07-02-active-venv.png)

![已激活的 Ruyi 虚拟环境放大截图](../assets/07-02-active-venv-zoom.png)

## 看一眼环境目录

```bash
find .ruyi-venv -maxdepth 2 -type f -o -type l
```

常见内容包括：

- `bin/`：工具链代理命令；选模拟器后还会有 `ruyi-qemu`。
- `sysroot/`：选择默认或其他 sysroot 来源后出现。
- `toolchain.cmake`：CMake 交叉编译工具链文件。
- `meson-cross.ini`：Meson cross file。
- `binfmt.conf`：加入模拟器后可能生成。


![Ruyi 虚拟环境目录](../assets/07-03-venv-files.png)

![Ruyi 虚拟环境目录的放大截图](../assets/07-03-venv-files-zoom.png)

## 停用与删除

- 点击当前环境名称或执行 `Ruyi: Deactivate Venv` 停用。



上一篇：[准备一个方便调试的 C 示例](06-example-project.md)  
下一篇：[交叉编译并检查 RISC-V ELF](08-build-and-elf.md)
