---
title: "Software-Setup"
description: "Vollständige Anleitung zur Softwareeinrichtung für die Openterface KVM-Erweiterung für uConsole."
keywords: "Openterface App Installation, uConsole Software, KVM App Installation, uConsole Konfiguration"
---

# **Software-Setup** | Openterface KVM-Erweiterung für uConsole

## Installationsübersicht

Die Openterface App ermöglicht Ihrer uConsole, als KVM-Schnittstelle zu fungieren, sodass Sie Zielgeräte über Bildschirm, Tastatur und Trackball steuern können.

!!! note "Anforderungen"
    - **uConsole**: Erfordert installierte Openterface App
    - **Ziel**: Keine App erforderlich – unterstützt Windows, macOS, Linux, Android, iOS
    - **Video**: Verwenden Sie ein Standard-HDMI-Kabel. Mit einem aktiven HDMI-Konverter werden auch Formate wie **VGA** und **DP** unterstützt. *Tipp: Stellen Sie sicher, dass der Konverter ausreichend mit Strom versorgt ist, sonst kann es zu einem schwarzen Bildschirm kommen.*

    - **Empfohlenes Video-Backend**: Für beste Leistung und Kompatibilität mit arm64-GPUs (z. B. Raspberry Pi) empfehlen wir **GStreamer** als Video-Backend. Beachten Sie, dass **Kali Linux** GStreamer möglicherweise nicht gut unterstützt.

## Installationsmethoden

### **Option 1: Download von GitHub Releases (Empfohlen für arm64)**

Laden Sie die neueste Openterface App für **arm64** direkt von unserer [GitHub Releases-Seite](https://github.com/TechxArtisanStudio/Openterface_QT/releases) herunter.

1. Besuchen Sie die [Openterface_QT Releases](https://github.com/TechxArtisanStudio/Openterface_QT/releases) Seite.
2. Laden Sie das neueste `.deb`-Paket für **arm64** herunter (z. B. `openterfaceqt_*_arm64.deb`).
3. Installieren Sie das Paket:
   ```bash
   sudo apt install ./openterfaceqt_*_arm64.deb
   ```
   *(Ersetzen Sie den Dateinamen gegebenenfalls durch den tatsächlichen Dateinamen.)*

---

### **Option 2: Flatpak-Installation**

Befolgen Sie unsere [Flatpak-Installationsanleitung](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md) für detaillierte Schritte.

---

### **Option 3: Community-Repository**

Wenn Sie den Community-Build von Rex bevorzugen:

1. **Repository hinzufügen**:
    ```bash
    wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
    sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
    ```

2. **Paket installieren**:
    ```bash
    sudo apt update
    sudo apt install openterfaceqt
    ```

!!! warning "Repository-Hinweis"
    Diese Befehle erfordern `sudo`. Das Repository richtet sich an arm64 Bookworm-Pakete; prüfen Sie die Kompatibilität mit Ihrem Gerät vor der Installation.

## Wichtige Hinweise

!!! tip "Stromversorgung & Erstinbetriebnahme"
    - **Stellen Sie sicher, dass Ihre uConsole ausreichend geladen ist oder an eine stabile Stromquelle angeschlossen ist.** Niedrige Spannung kann zu unzuverlässigem Betrieb oder Verbindungsproblemen führen.
    - **Wenn Sie beim ersten Versuch das Zielgerät nicht steuern können:**
        1. Schalten Sie die uConsole vollständig aus.
        2. Warten Sie mindestens 10 Sekunden.
        3. Schalten Sie sie wieder ein und versuchen Sie es erneut.
    Dies kann helfen, die Hardware zu initialisieren und Verbindungsprobleme beim ersten Start zu beheben.

!!! tip "Serielle Kommunikation Baudrate"
    - **Stellen Sie die Baudrate auf 9600** ein, wenn Sie serielle Kommunikation verwenden. Dies reduziert Fehler, da die uConsole oft nicht genug Leistung liefert, um 115200 zuverlässig zu halten.

## Gebrauchsanleitung

### **Starten der KVM-Sitzung**
1. Starten Sie die Openterface App auf Ihrer uConsole
2. Die App erkennt automatisch die KVM-Erweiterungsplatine
3. Verbinden Sie Ihr Zielgerät über HDMI
4. Verwenden Sie die eingebaute Tastatur und den Trackball der uConsole, um das Zielgerät zu steuern

### **Steuerfunktionen**
- **Tastatur**: Volle Tastatur-Emulation einschließlich Multimedia-Tasten
- **Maus**: Absolute und relative Mauspositionierung
- **Audio**: HDMI-Audio-Passthrough zu den uConsole-Lautsprechern

### **Erweiterte Funktionen**
- **Textübertragung**: Schnelles Übertragen von Text durch Simulieren von Tastenanschlägen—ideal für Benutzernamen, Passwörter und Code-Snippets
- **Umschaltbares USB**: Wechseln Sie einfach den USB-Zugriff zwischen der uConsole und dem Zielgerät über die Host-App
---
title: "Software-Setup"
description: "Vollständiger Software-Setup-Leitfaden für Openterface KVM Extension for uConsole. Lernen Sie, wie Sie die Openterface App auf Ihrem uConsole installieren und konfigurieren für nahtlose KVM-Funktionalität."
keywords: "Openterface App Installation, uConsole Software Setup, KVM App Setup, uConsole App Konfiguration, Software Installation Guide"
---

# **Software-Setup** | Openterface KVM Extension for uConsole

## Installationsübersicht

Die Openterface App ermöglicht es Ihrem uConsole, als KVM-Interface zu fungieren, sodass Sie Zielgeräte über den eingebauten Bildschirm, die Tastatur und das Trackball steuern können.

!!! note "Anforderungen"
    - **uConsole**: Erfordert Installation der Openterface App
    - **Ziel**: Keine App erforderlich - unterstützt Windows, macOS, Linux, Android, iOS
    - **Video**: Verwenden Sie ein Standard-HDMI-Kabel. Verwenden Sie ein Standard-HDMI-Kabel. Mit einem netzbetriebenen HDMI-Konverter unterstützt es auch andere Formate wie **VGA**, **DP** und mehr. *Tipp: Stellen Sie sicher, dass der Konverter ordnungsgemäß mit Strom versorgt wird; andernfalls können Sie einen schwarzen Bildschirm erleben.*

## Installationsmethoden

### **Option 1: Flatpak-Installation**

Folgen Sie unserem [Flatpak-Installationsleitfaden](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md) für detaillierte Setup-Schritte.

### **Option 2: Community-Repository (Empfohlen)**

Wenn Sie die von Rex gepflegte Community-Build bevorzugen:

1. **Repository hinzufügen**:
```bash
wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
```

2. **Paket installieren**:
```bash
sudo apt update
sudo apt install openterfaceqt
```

!!! warning "Repository-Hinweise"
    Diese Befehle erfordern sudo. Das Repository zielt auf arm64 Bookworm-Pakete ab; überprüfen Sie die Kompatibilität mit Ihrem Gerät vor der Installation.

## Verwendungsanweisungen

### **KVM-Sitzung starten**
1. Starten Sie die Openterface App auf Ihrem uConsole
2. Die App erkennt automatisch die KVM Extension-Karte
3. Verbinden Sie Ihr Zielgerät über HDMI
4. Verwenden Sie die eingebaute Tastatur und das Trackball des uConsole, um das Zielgerät zu steuern

### **Steuerungsfunktionen**
- **Tastatur**: Vollständige Tastaturemulation einschließlich Multimediatasten
- **Maus**: Absolute und relative Mauspositionierung
- **Audio**: HDMI-Audio-Durchgang zu uConsole-Lautsprechern

### **Erweiterte Funktionen**
- **Textübertragung**: Übertragen Sie schnell Text durch Simulation von Tastenanschlägen—ideal für Benutzernamen, Passwörter und Codeschnipsel
- **Umschaltbares USB**: Wechseln Sie einfach den USB-Zugriff zwischen uConsole und Zielgerät über die Host-App
