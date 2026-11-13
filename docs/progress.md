# 实验进度

更新时间：2026-11-13（Asia/Shanghai）

## 当前结论

- 正式实验目录：`D:\2026\2026秋\轻量级匿名凭证`。
- Windows 主机约 16GB RAM，硬件虚拟化/Hyper-V 已启用。
- WSL 版本 2.3.17.0；已安装 `Ubuntu-22.04` 与 `kali-linux`，两者均为 WSL2。本项目固定使用 Ubuntu 22.04。
- Ubuntu 22.04 能正常启动；WSL 可见内存约 7.4GiB。
- Ubuntu 已有 Rust/Cargo 1.99.0、Git 2.34.1、CMake 4.4.4、Ninja；尚未发现 `qemu-system-arm`。
- Windows 已有 Git 2.46.0 与 Python 3.11.9；未发现 Windows 侧 Rust/QEMU，且本项目不要求在 Windows 原生侧构建。
- 工作区初检为空，未发现既有实验工程、数据或 Git 元数据。
- 用户将为该目录建立 Git 私有仓库；在远程仓库建立前，本地实验可继续。
- 用户提供的 ChatGPT 分享链接当前无法由自动读取器取回；已确认的需求以用户消息和 `AGENTS.md` 为准，不阻塞实验。

## 已完成

- [x] 明确唯一正式环境与第一阶段边界。
- [x] 检查 Windows、WSL2 发行版、虚拟化、内存和现有工具。
- [x] 固化长期约定和第一阶段验收口径。

## 正在进行

- [ ] 检查 Ubuntu 包管理权限并安装 QEMU ARM system emulator。
- [ ] 安装 Rust 目标 `thumbv7em-none-eabi`。
- [ ] 精确确认 `zkmcu-verifier 0.1.0` API、wire format 与 Cortex-M4 编译兼容性。
- [ ] 建立 arkworks 主机生成器、Cortex-M4 固件和可重放脚本。

## 第一阶段验收清单

- [ ] 主机为 `x=3, y=9` 生成证明并由 arkworks 原生验证。
- [ ] QEMU `mps2-an386` 上正确证明通过。
- [ ] 同一证明的公开值改为 `10` 后被拒绝。
- [ ] 非法编码返回错误且不 panic。
- [ ] 256 KiB 配置连续运行三次，保存原始日志和环境版本。
- [ ] 分别记录静态区、heap 容量/峰值、stack 高水位，避免重复计数。
- [ ] 尝试 128 KiB，再探索更小 RAM。

## 风险与记录

- QEMU 仿真时间不能作为真实 MCU 时间；这里只记录其功能结果和宿主侧运行时间（若记录，须明确标注为非 MCU 性能）。
- `zkmcu-verifier 0.1.0` 官方示例主要面向 Cortex-M33/RP2350；本项目的 Cortex-M4/QEMU 适配需单独验证。
- 当前 WSL 从 Windows 受限进程内枚举发行版曾返回 `E_ACCESSDENIED`，在获准的主机检查中已确认 WSL2 正常，属于会话权限差异而非 WSL 故障。

