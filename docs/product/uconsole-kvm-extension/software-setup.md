---
title: "Software Setup"
description: "Complete software setup guide for Openterface KVM Extension for uConsole. Learn how to install and configure the Openterface App on your uConsole for seamless KVM functionality."
keywords: "Openterface app installation, uConsole software setup, KVM app setup, uConsole app configuration, software installation guide"
---

# **Software Setup** | Openterface KVM Extension for uConsole

## Installation Overview

The Openterface App enables your uConsole to function as a KVM interface, allowing you to control target devices through the built-in screen, keyboard, and trackball.

!!! note "Requirements"
    - **uConsole**: Requires Openterface App installed
    - **Target**: No app needed - supports Windows, macOS, Linux, Android, iOS
    - **Video**: Use standard HDMI cable. With a powered HDMI converter, it also supports other formats such as **VGA**, **DP**, and more. *Tip: Ensure the converter is properly powered; otherwise, you may experience a black screen.*
    - **Recommended Video Backend**: For best performance and compatibility with arm64 GPUs (such as in the Raspberry Pi ecosystem), use **GStreamer** as the video backend. However, please note that **Kali Linux** may not support GStreamer well.

## Installation Methods

### **Option 1: Download from GitHub Releases (Recommended for arm64)**

Download the latest Openterface App release for **arm64** directly from our [GitHub Releases page](https://github.com/TechxArtisanStudio/Openterface_QT/releases).

1. Visit the [Openterface_QT Releases](https://github.com/TechxArtisanStudio/Openterface_QT/releases) page.
2. Download the latest `.deb` package for **arm64** (e.g., `openterfaceqt_*_arm64.deb`).
3. Install the package:
    ```bash
    sudo apt install ./openterfaceqt_*_arm64.deb
    ```
    *(Replace the filename with the actual downloaded file name if different.)*

---

### **Option 2: Flatpak Installation**

Follow our [Flatpak Installation Guide](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md) for detailed setup steps.

---

### **Option 3: Community Repository**

If you prefer the community build maintained by Rex:

1. **Add Repository**:
    ```bash
    wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
    sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
    ```

2. **Install Package**:
    ```bash
    sudo apt update
    sudo apt install openterfaceqt
    ```

!!! warning "Repository Notes"
     These commands require sudo. The repository targets arm64 Bookworm packages; verify compatibility with your device before installing.



## Important Reminders

!!! tip "Power & First-Time Setup"
    - **Ensure your uConsole is sufficiently charged or connected to a stable power source.** Low power may cause unreliable operation or connection issues.
    - **If you cannot control the target device on your first attempt:**
        1. Fully shut down the uConsole.
        2. Wait at least 10 seconds.
        3. Power it on again and retry.
    This can help initialize the hardware and resolve first-time connection issues.

!!! tip "Serial Communication Baudrate"
    - **Set the baudrate to 9600** when using serial communication. This helps reduce error rates, as the uConsole often cannot deliver enough power to reliably maintain 115200 baudrate.

## Usage Instructions

### **Starting the KVM Session**
1. Launch the Openterface App on your uConsole
2. The app will automatically detect the KVM Extension board
3. Connect your target device via HDMI
4. Use uConsole's built-in keyboard and trackball to control the target device

### **Control Features**
- **Keyboard**: Full keyboard emulation including multimedia keys
- **Mouse**: Absolute and relative mouse positioning
- **Audio**: HDMI audio passthrough to uConsole speakers

### **Advanced Features**
- **Text Transfer**: Quickly transmit text by simulating keystrokes—ideal for usernames, passwords, and code snippets
- **Switchable USB**: Easily switch USB access between the uConsole and the target device using the host app