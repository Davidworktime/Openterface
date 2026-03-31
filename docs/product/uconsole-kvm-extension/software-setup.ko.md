---
title: "소프트웨어 설치"
description: "uConsole용 Openterface KVM 확장 소프트웨어 설치 가이드입니다."
keywords: "Openterface 앱 설치, uConsole 소프트웨어, KVM 설정, uConsole 구성"
---

# **소프트웨어 설치** | uConsole용 Openterface KVM 확장

## 설치 개요

Openterface 앱은 uConsole을 KVM 인터페이스로 사용하여 내장 화면, 키보드, 트랙볼로 대상 기기를 제어할 수 있게 합니다.

!!! note "요구사항"
    - **uConsole**: Openterface 앱 설치 필요
    - **대상기기**: 앱 불필요 — Windows, macOS, Linux, Android, iOS 지원
    - **비디오**: 표준 HDMI 케이블을 사용하세요. 전원 공급형 HDMI 변환기를 사용하면 **VGA**, **DP** 등도 지원합니다. *팁: 변환기에 충분한 전원이 공급되는지 확인하세요. 그렇지 않으면 검은 화면이 나타날 수 있습니다.*

    - **권장 비디오 백엔드**: arm64 GPU(예: Raspberry Pi)와의 호환 및 성능을 위해 비디오 백엔드로 **GStreamer** 사용을 권장합니다. 다만 **Kali Linux**에서는 GStreamer 지원이 원활하지 않을 수 있습니다.

## 설치 방법

### **옵션 1: GitHub Releases에서 다운로드 (arm64 권장)**

최신 Openterface 앱 **arm64** 릴리스를 [GitHub Releases](https://github.com/TechxArtisanStudio/Openterface_QT/releases)에서 직접 다운로드하세요.

1. [Openterface_QT Releases](https://github.com/TechxArtisanStudio/Openterface_QT/releases) 페이지로 이동합니다.
2. **arm64**용 최신 `.deb` 패키지(예: `openterfaceqt_*_arm64.deb`)를 다운로드합니다.
3. 패키지 설치:
   ```bash
   sudo apt install ./openterfaceqt_*_arm64.deb
   ```
   *(파일명이 다르면 실제 파일명으로 바꾸세요.)*

---

### **옵션 2: Flatpak 설치**

자세한 단계는 [Flatpak 설치 가이드](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md)를 참조하세요.

---

### **옵션 3: 커뮤니티 리포지토리**

Rex가 유지 관리하는 커뮤니티 빌드를 사용하려면:

1. **저장소 추가**:
    ```bash
    wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
    sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
    ```

2. **패키지 설치**:
    ```bash
    sudo apt update
    sudo apt install openterfaceqt
    ```

!!! warning "저장소 주의"
    이 명령은 `sudo` 권한이 필요합니다. 해당 저장소는 arm64 Bookworm 패키지를 대상으로 하므로 설치 전 기기 호환성을 확인하세요.

## 중요한 알림

!!! tip "전원 및 초기 설정"
    - **uConsole이 충분히 충전되었거나 안정적인 전원에 연결되어 있는지 확인하세요.** 전압 부족은 불안정한 동작이나 연결 문제를 일으킬 수 있습니다.
    - **처음에 대상 기기를 제어할 수 없는 경우:**
        1. uConsole을 완전히 종료합니다.
        2. 최소 10초간 기다립니다.
        3. 다시 전원을 켜고 재시도하세요.

!!! tip "시리얼 통신 보오레이트"
    - 시리얼 통신 시 **9600 보오레이트**로 설정하세요. uConsole은 종종 115200을 안정적으로 유지할 만큼 전력을 제공하지 못해 오류율이 높아질 수 있습니다.

## 사용 방법

### **KVM 세션 시작**
1. uConsole에서 Openterface 앱을 실행합니다
2. 앱이 KVM 확장 보드를 자동으로 감지합니다
3. HDMI로 대상 기기를 연결합니다
4. uConsole의 내장 키보드와 트랙볼로 대상 기기를 제어합니다

### **제어 기능**
- **키보드**: 멀티미디어 키를 포함한 전체 키보드 에뮬레이션
- **마우스**: 절대 및 상대 마우스 위치 지정
- **오디오**: HDMI 오디오 패스스루를 uConsole 스피커로 전달

### **고급 기능**
- **텍스트 전송**: 키 입력을 시뮬레이트해 텍스트를 빠르게 전송—사용자 이름, 비밀번호, 코드 스니펫에 적합
- **전환 가능한 USB**: 호스트 앱을 통해 uConsole과 대상 기기 간 USB 접근을 전환할 수 있습니다
---
title: "소프트웨어 설정"
description: "Openterface KVM Extension for uConsole의 완전한 소프트웨어 설정 가이드입니다. 원활한 KVM 기능을 위해 uConsole에 Openterface App을 설치하고 구성하는 방법을 배워보세요."
keywords: "Openterface 앱 설치, uConsole 소프트웨어 설정, KVM 앱 설정, uConsole 앱 구성, 소프트웨어 설치 가이드"
---

# **소프트웨어 설정** | Openterface KVM Extension for uConsole

## 설치 개요

Openterface App은 uConsole이 KVM 인터페이스로 작동할 수 있게 하여 내장 화면, 키보드 및 트랙볼을 통해 대상 장치를 제어할 수 있습니다.

!!! note "요구사항"
    - **uConsole**: Openterface App 설치 필요
    - **대상 장치**: 앱 불필요 - Windows, macOS, Linux, Android, iOS 지원
    - **비디오**: 표준 HDMI 케이블을 사용하세요. 표준 HDMI 케이블을 사용하세요. 전원이 공급되는 HDMI 변환기를 사용하면 **VGA**, **DP** 등의 다른 형식도 지원합니다. *팁: 변환기가 적절히 전원 공급되는지 확인하세요. 그렇지 않으면 검은 화면이 나타날 수 있습니다.*

## 설치 방법

### **옵션 1: Flatpak 설치**

자세한 설정 단계는 [Flatpak 설치 가이드](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md)를 따르세요.

### **옵션 2: 커뮤니티 저장소 (권장)**

Rex가 유지 관리하는 커뮤니티 빌드를 선호하는 경우:

1. **저장소 추가**:
```bash
wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
```

2. **패키지 설치**:
```bash
sudo apt update
sudo apt install openterfaceqt
```

!!! warning "저장소 참고사항"
    이러한 명령은 sudo가 필요합니다. 저장소는 arm64 Bookworm 패키지를 대상으로 합니다. 설치 전에 장치와의 호환성을 확인하세요.

## 사용 지침

### **KVM 세션 시작**
1. uConsole에서 Openterface App 실행
2. 앱이 자동으로 KVM Extension 보드를 감지
3. HDMI를 통해 대상 장치 연결
4. uConsole의 내장 키보드와 트랙볼을 사용하여 대상 장치 제어

### **제어 기능**
- **키보드**: 멀티미디어 키를 포함한 전체 키보드 에뮬레이션
- **마우스**: 절대 및 상대 마우스 위치
- **오디오**: HDMI 오디오를 uConsole 스피커로 패스스루

### **고급 기능**
- **텍스트 전송**: 키 입력을 시뮬레이션하여 텍스트를 빠르게 전송—사용자명, 비밀번호, 코드 스니펫에 이상적
- **전환 가능한 USB**: 호스트 앱을 사용하여 uConsole과 대상 장치 간에 USB 액세스를 쉽게 전환
