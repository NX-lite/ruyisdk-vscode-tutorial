# 【RuyiSDK VS Code 扩展】Linux 篇 08：交叉编译并检查 RISC-V ELF

> 本篇标签：`RuyiSDK`、`Linux`、`VS Code`、`RISC-V`、`交叉编译`、`上手记录`


## 构建前确认

- `examples/hello-ruyi` 是工作区根目录。
- 状态栏显示 `hello-riscv` venv 已激活。
- 新终端中能找到 `riscv64-unknown-linux-gnu-gcc`。
- 根目录存在 `Makefile`。

先清理旧产物：

```bash
make clean
```

## 使用扩展构建

任选一个入口：

- 状态栏左下角 `Build`；
- 编辑器标题栏 `Build Project`；
- 命令面板 `Ruyi: Build Project`。

打开“输出”，下拉选择 `RuyiSDK Build`。日志应该包含：

- 命中的 GNU Make 构建规则；
- 当前 venv 名称；
- Workdir；
- 实际 Command；
- 成功时的 `Build succeeded`。


![Ruyi Build Project 入口](./assets/images/08-01-build-entry.png)

![Ruyi Build Project 入口的放大截图](./assets/images/08-01-build-entry-zoom.png)

![RuyiSDK Build 输出面板](./assets/images/08-02-build-output.png)

![RuyiSDK Build 输出面板的放大截图](./assets/images/08-02-build-output-zoom.png)

## 检查产物

在集成终端执行：

```bash
file ./hello-riscv
readelf -h ./hello-riscv
readelf -S ./hello-riscv | grep -E 'debug_info|symtab'
```

关键字段应包括：

```text
ELF 64-bit
Machine: RISC-V
statically linked
with debug_info
not stripped
```


![RISC-V ELF 检查结果](./assets/images/08-03-elf-inspection.png)

![RISC-V ELF 检查结果的放大截图](./assets/images/08-03-elf-inspection-zoom.png)

## 扩展如何选择构建规则

默认优先级是：

1. 根目录 `CMakeLists.txt` → CMake；
2. `Makefile`、`GNUmakefile` 或 `makefile` → GNU Make；
3. 根目录 `*.c` → GCC C。


- Makefile 仍要自己设置 `CC`/`CXX`；
- CMake 项目仍要指定 `CMAKE_TOOLCHAIN_FILE`、Preset 或缓存；
- 未激活 venv 时会使用 Host 环境中的工具。




上一篇：[创建并激活 Ruyi 虚拟环境](07-ruyi-venv.md)  
下一篇：[用 QEMU 运行程序](09-qemu-run.md)
