# 小节索引与写作约定

这个目录用来放拆分后的正文。仓库首页只维护总路线、章节安排和完成状态，具体操作分别写进对应小节，避免所有内容挤在一个 README 里。

## 正文目录

| 编号 | 标题 | 验证状态 |
| --- | --- | --- |
| 01 | [准备 VS Code 或 VSCodium](01-ide-setup.md) | 已实测 |
| 02 | [安装 RuyiSDK 扩展](02-extension-install.md) | 已实测 |
| 03 | [让扩展找到 Ruyi](03-ruyi-setup.md) | 已实测 |
| 04 | [先逛一遍欢迎页和常用功能](04-extension-tour.md) | 待复测 |
| 05 | [安装 GNU 工具链、QEMU 和基础工具](05-toolchain-qemu.md) | 已实测 |
| 06 | [准备一个方便调试的 C 示例](06-example-project.md) | 已实测 |
| 07 | [创建并激活 Ruyi 虚拟环境](07-ruyi-venv.md) | 已实测 |
| 08 | [交叉编译并检查 RISC-V ELF](08-build-and-elf.md) | 已实测 |
| 09 | [用 QEMU 运行程序](09-qemu-run.md) | 已实测 |
| 10 | [用 QEMU 和 GDB 调试程序](10-qemu-gdb.md) | 已实测 |

## 文件命名

正文文件使用 `两位编号-英文短名.md`：

```text
01-ide-setup.md
02-extension-install.md
03-ruyi-setup.md
04-extension-tour.md
05-toolchain-qemu.md
06-example-project.md
07-ruyi-venv.md
08-build-and-elf.md
09-qemu-run.md
10-qemu-gdb.md
```

图片放在 `assets/images/`，使用 `小节编号-两位序号-内容短名.png`，例如 `04-01-home.png`、`08-02-elf-header.png`。同一小节新增图片时只追加序号，避免修改正文里已有的链接。

## 系列名称、标题和标签

系列名称统一为“Linux 下 RuyiSDK VS Code 扩展上手记录”。单篇一级标题采用下面的格式：

```text
# 【RuyiSDK VS Code 扩展】Linux 篇 04：先逛一遍欢迎页和常用功能
```

固定标签使用 `RuyiSDK`、`Linux`、`VS Code`、`RISC-V`、`上手记录`。再根据单篇内容补充 `VSCodium`、`QEMU`、`GDB`、`交叉编译` 或 `开发板`，不为凑数量添加无关标签。

## 正文模板

小节不要求每次把模板中的标题全部写出来，只保留确实有内容的部分。

```markdown
# 【RuyiSDK VS Code 扩展】Linux 篇 NN：这一节要完成的事

用两三句话说明我为什么做这一步，以及做完后接着做什么。

> 状态：待实测 / 已实测 / 待复测 / 待设备
>
> 实测版本：IDE、RuyiSDK 扩展、Ruyi
>
> 本篇标签：固定标签 + 与本篇内容相关的补充标签

## 我用的环境

## 实际操作

## 我看到的结果

## 遇到问题时

## 相关链接
```

命令输出只截取帮助判断结果的部分。暂时没有设备或还没走通的地方直接保留状态，等复测后再补命令和截图。
