# Linux 下 RuyiSDK VS Code 扩展上手记录

这是我整理 RuyiSDK VS Code 扩展使用过程时留下的实操记录，面向第一次接触 RuyiSDK 的同学。它不是官方教程；命令和截图都带着我当时使用的版本，插件升级后，个别菜单名称或界面位置可能会变化。

这个仓库会按实际写作进度更新。目前先发布环境准备、扩展安装和 Ruyi 路径配置三篇，后续再补工具链、虚拟环境、交叉编译、QEMU 和 GDB。

## 已发布

| 编号 | 内容 | 状态 |
| --- | --- | --- |
| 01 | [准备 VS Code 或 VSCodium](docs/01-ide-setup.md) | 已实测 |
| 02 | [安装 RuyiSDK 扩展](docs/02-extension-install.md) | 已实测 |
| 03 | [让扩展找到 Ruyi](docs/03-ruyi-setup.md) | 已实测 |

第一次阅读可以从第 01 篇开始。如果 VS Code 和扩展已经装好，也可以直接看第 03 篇的自动检测和手动路径设置。

## 后续路线

```text
准备 VS Code / VSCodium
  → 安装 RuyiSDK VS Code 扩展
  → 检测、安装或指定 ruyi 可执行文件
  → 认识欢迎页、Packages、Virtual Environments 和 News
  → 安装 GNU 工具链、QEMU 与基础工具
  → 创建示例工程和 Ruyi 虚拟环境
  → 交叉编译并检查 RISC-V ELF
  → 使用 QEMU 运行
  → 使用 QEMU + GDB 调试
```

## 截图环境

前三篇截图来自 Arch Linux/x86_64，使用 VS Code 1.111.0、Ruyi 0.50.0 和 RuyiSDK 扩展 0.1.5。版本号不必和截图相同，但建议在操作前记下自己的 IDE、扩展、Ruyi 和 Host 架构，遇到问题时更容易对照。

## 参考资料

- [RuyiSDK VS Code 扩展文档](https://ruyisdk.org/docs/VSCode-Plugins/)
- [Ruyi 包管理器安装文档](https://ruyisdk.org/docs/Package-Manager/installation/)
- [RuyiSDK 下载页](https://ruyisdk.org/downloads/)
- [RuyiSDK VS Code 扩展仓库](https://github.com/ruyisdk/ruyisdk-vscode-extension)

## License

本仓库使用 [MIT License](LICENSE)。
