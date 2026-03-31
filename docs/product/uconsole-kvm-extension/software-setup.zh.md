---
title: "软件安装"
description: "Openterface KVM 扩展（适用于 uConsole）的完整软件安装与配置指南。"
keywords: "Openterface 应用 安装, uConsole 软件, KVM 应用 安装, uConsole 配置"
---

# **软件安装** | 适用于 uConsole 的 Openterface KVM 扩展

## 安装概览

Openterface 应用使您的 uConsole 能作为 KVM 接口使用，可通过内置屏幕、键盘和轨迹球控制目标设备。

!!! note "要求"
    - **uConsole**：需要安装 Openterface 应用
    - **目标设备**：无需安装应用 — 支持 Windows、macOS、Linux、Android、iOS
    - **视频**：请使用标准 HDMI 线。使用带电源的 HDMI 转换器可支持 **VGA**、**DP** 等格式。*提示：请确认转换器有足够电源，否则可能出现黑屏。*

    - **推荐视频后端**：为获得最佳性能并兼容 arm64 GPU（如 Raspberry Pi 生态），建议使用 **GStreamer** 作为视频后端。但请注意 **Kali Linux** 可能不支持 GStreamer。

## 安装方式

### **选项1：从 GitHub Releases 下载（推荐 arm64）**

直接从我们的 [GitHub Releases 页面](https://github.com/TechxArtisanStudio/Openterface_QT/releases) 下载最新的 **arm64** 版本。

1. 访问 [Openterface_QT Releases](https://github.com/TechxArtisanStudio/Openterface_QT/releases) 页面。
2. 下载最新的 **arm64** `.deb` 包（例如 `openterfaceqt_*_arm64.deb`）。
3. 安装包：
   ```bash
   sudo apt install ./openterfaceqt_*_arm64.deb
   ```
   *(如文件名不同请替换为实际文件名。)*

---

### **选项2：Flatpak 安装**

请参阅我们的 [Flatpak 安装指南](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md) 获取详细步骤。

---

### **选项3：社区仓库**

如果您更倾向于使用 Rex 维护的社区构建：

1. **添加仓库**：
    ```bash
    wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
    sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
    ```

2. **安装软件包**：
    ```bash
    sudo apt update
    sudo apt install openterfaceqt
    ```

!!! warning "仓库说明"
    这些命令需要 `sudo` 权限。该仓库面向 arm64 Bookworm 包；在安装前请确认与设备的兼容性。

## 重要提醒

!!! tip "电源与首次启动"
    - **确保 uConsole 已充足电或连接稳定电源。** 电量不足会导致运行不稳定或连接问题。
    - **如果首次无法控制目标设备：**
        1. 完全关机 uConsole。
        2. 等待至少 10 秒。
        3. 重新开机并重试。
    这有助于初始化硬件并解决首次连接问题。

!!! tip "串口通信波特率"
    - **在使用串口通信时请设置波特率为 9600。** 这可以降低错误率，因为 uConsole 通常无法提供足够电力来稳定维持 115200 波特率。

## 使用说明

### **启动 KVM 会话**
1. 在 uConsole 上启动 Openterface 应用
2. 应用将自动检测 KVM 扩展板
3. 通过 HDMI 连接目标设备
4. 使用 uConsole 的内置键盘和轨迹球来控制目标设备

### **控制功能**
- **键盘**：完整的键盘仿真，包括多媒体键
- **鼠标**：支持绝对与相对鼠标定位
- **音频**：HDMI 音频直通到 uConsole 扬声器

### **高级功能**
- **文本传输**：通过模拟按键快速发送文本——适用于用户名、密码和代码片段
- **可切换 USB**：通过主机应用在 uConsole 与目标设备之间切换 USB 访问
---
title: "软件设置"
description: "Openterface KVM Extension for uConsole 的完整软件设置指南。学习如何在您的 uConsole 上安装和配置 Openterface App，以实现无缝 KVM 功能。"
keywords: "Openterface应用安装, uConsole软件设置, KVM应用设置, uConsole应用配置, 软件安装指南"
---

# **软件设置** | Openterface KVM Extension for uConsole

## 安装概述

Openterface App 使您的 uConsole 能够作为 KVM 接口运行，允许您通过内置屏幕、键盘和轨迹球控制目标设备。

!!! note "要求"
    - **uConsole**：需要安装 Openterface App
    - **目标设备**：无需应用 - 支持 Windows、macOS、Linux、Android、iOS
    - **视频**：使用标准 HDMI 电缆。使用标准 HDMI 电缆。通过供电的 HDMI 转换器，它还支持其他格式，如 **VGA**、**DP** 等。*提示：确保转换器正确供电；否则，您可能会遇到黑屏。*

## 安装方法

### **选项 1：Flatpak 安装**

按照我们的 [Flatpak 安装指南](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md) 进行详细的设置步骤。

### **选项 2：社区仓库（推荐）**

如果您更喜欢 Rex 维护的社区构建：

1. **添加仓库**：
```bash
wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
```

2. **安装包**：
```bash
sudo apt update
sudo apt install openterfaceqt
```

!!! warning "仓库说明"
    这些命令需要 sudo。仓库针对 arm64 Bookworm 包；安装前请验证与您设备的兼容性。

## 使用说明

### **启动 KVM 会话**
1. 在您的 uConsole 上启动 Openterface App
2. 应用将自动检测 KVM Extension 板
3. 通过 HDMI 连接您的目标设备
4. 使用 uConsole 的内置键盘和轨迹球控制目标设备

### **控制功能**
- **键盘**：完整键盘模拟，包括多媒体键
- **鼠标**：绝对和相对鼠标定位
- **音频**：HDMI 音频直通到 uConsole 扬声器

### **高级功能**
- **文本传输**：通过模拟按键快速传输文本—非常适合用户名、密码和代码片段
- **可切换 USB**：使用主机应用轻松在 uConsole 和目标设备之间切换 USB 访问
