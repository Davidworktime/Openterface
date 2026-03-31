---
title: "Configurare Software"
description: "Ghid complet de configurare software pentru extensia KVM Openterface pentru uConsole."
keywords: "instalare Openterface, software uConsole, configurare KVM, instalare aplicație"
---

# **Configurare Software** | Extensia KVM Openterface pentru uConsole

## Prezentare instalare

Aplicația Openterface permite uConsole-ului să funcționeze ca interfață KVM, permițând controlul dispozitivelor țintă prin ecranul, tastatura și trackball-ul încorporate.

!!! note "Cerințe"
    - **uConsole**: Necesită aplicația Openterface instalată
    - **Țintă**: Nu este necesară nicio aplicație — suportă Windows, macOS, Linux, Android, iOS
    - **Video**: Folosiți un cablu HDMI standard. Cu un convertor HDMI alimentat, suportă și formate precum **VGA** și **DP**. *Sfat: Asigurați-vă că convertorul are alimentare adecvată; altfel, s-ar putea afișa ecran negru.*

    - **Backend video recomandat**: Pentru performanță și compatibilitate optimă cu GPU-urile arm64 (ex. Raspberry Pi), folosiți **GStreamer** ca backend video. Rețineți că **Kali Linux** poate să nu suporte bine GStreamer.

## Metode de instalare

### **Opțiunea 1: Descărcare de pe GitHub Releases (Recomandat pentru arm64)**

Descărcați cea mai recentă versiune a aplicației Openterface pentru **arm64** direct de pe pagina noastră de [GitHub Releases](https://github.com/TechxArtisanStudio/Openterface_QT/releases).

1. Vizitați pagina [Openterface_QT Releases](https://github.com/TechxArtisanStudio/Openterface_QT/releases).
2. Descărcați pachetul `.deb` cel mai recent pentru **arm64** (ex. `openterfaceqt_*_arm64.deb`).
3. Instalați pachetul:
   ```bash
   sudo apt install ./openterfaceqt_*_arm64.deb
   ```
   *(Înlocuiți numele fișierului după caz.)*

---

### **Opțiunea 2: Instalare Flatpak**

Urmăriți [Ghidul de instalare Flatpak](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md) pentru pași detaliați.

---

### **Opțiunea 3: Repozitoriu comunitar**

Dacă preferați build-ul comunitar întreținut de Rex:

1. **Adăugați repozitoriul**:
    ```bash
    wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
    sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
    ```

2. **Instalați pachetul**:
    ```bash
    sudo apt update
    sudo apt install openterfaceqt
    ```

!!! warning "Notă despre repozitoriu"
    Aceste comenzi necesită `sudo`. Repozitoriul vizează pachete arm64 Bookworm; verificați compatibilitatea cu dispozitivul dvs. înainte de instalare.

## Mementouri importante

!!! tip "Alimentare & prima pornire"
    - **Asigurați-vă că uConsole este suficient încărcată sau conectată la o sursă de alimentare stabilă.** Alimentarea scăzută poate cauza comportament nefiabil sau probleme de conexiune.
    - **Dacă nu puteți controla dispozitivul țintă la prima încercare:**
        1. Opriți complet uConsole.
        2. Așteptați cel puțin 10 secunde.
        3. Porniți din nou și încercați din nou.

!!! tip "Baudrate comunicare serială"
    - **Setați baudrate-ul la 9600** când folosiți comunicare serială. Aceasta reduce rata de erori, deoarece uConsole adesea nu poate furniza suficientă putere pentru a menține 115200 în mod fiabil.

## Instrucțiuni de utilizare

### **Pornire sesiune KVM**
1. Lansați aplicația Openterface pe uConsole
2. Aplicația va detecta automat placa de extensie KVM
3. Conectați dispozitivul țintă prin HDMI
4. Folosiți tastatura și trackball-ul integrate pentru a controla dispozitivul

### **Funcții de control**
- **Tastatură**: Emulare completă a tastaturii, inclusiv taste multimedia
- **Mouse**: Poziționare absolută și relativă a mouse-ului
- **Audio**: Passthrough audio HDMI către difuzoarele uConsole

### **Funcții avansate**
- **Transfer text**: Trimiteți text rapid simulând apăsări de taste — ideal pentru nume de utilizator, parole și fragmente de cod
- **USB comutabil**: Comutați ușor accesul USB între uConsole și dispozitivul țintă prin aplicația host
---
title: "Configurare software"
description: "Ghid complet de configurare software pentru Openterface KVM Extension for uConsole. Învață cum să instalezi și să configurezi App-ul Openterface pe uConsole-ul tău pentru funcționalitate KVM fără probleme."
keywords: "instalare app Openterface, configurare software uConsole, configurare app KVM, configurare app uConsole, ghid instalare software"
---

# **Configurare software** | Openterface KVM Extension for uConsole

## Prezentare generală instalare

App-ul Openterface permite uConsole-ului tău să funcționeze ca o interfață KVM, permițându-ți să controlezi dispozitivele țintă prin ecranul integrat, tastatura și trackball.

!!! note "Cerințe"
    - **uConsole**: Necesită instalarea App-ului Openterface
    - **Țintă**: Nu este necesar app - suportă Windows, macOS, Linux, Android, iOS
    - **Video**: Folosește un cablu HDMI standard. Folosește un cablu HDMI standard. Cu un convertor HDMI alimentat, suportă și alte formate precum **VGA**, **DP** și mai multe. *Sfat: Asigură-te că convertorul este alimentat corespunzător; altfel, poți experimenta un ecran negru.*

## Metode de instalare

### **Opțiunea 1: Instalare Flatpak**

Urmărește [Ghidul nostru de instalare Flatpak](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md) pentru pași de configurare detaliați.

### **Opțiunea 2: Depozitarul comunității (Recomandat)**

Dacă preferi build-ul comunității întreținut de Rex:

1. **Adaugă depozitarul**:
```bash
wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
```

2. **Instalează pachetul**:
```bash
sudo apt update
sudo apt install openterfaceqt
```

!!! warning "Note depozitar"
    Aceste comenzi necesită sudo. Depozitarul țintește pachete arm64 Bookworm; verifică compatibilitatea cu dispozitivul tău înainte de instalare.

## Instrucțiuni de utilizare

### **Pornirea sesiunii KVM**
1. Lansează App-ul Openterface pe uConsole-ul tău
2. App-ul va detecta automat placa Extension KVM
3. Conectează dispozitivul tău țintă prin HDMI
4. Folosește tastatura și trackball-ul integrat ale uConsole-ului pentru a controla dispozitivul țintă

### **Funcționalități de control**
- **Tastatură**: Emulare completă a tastaturii incluzând taste multimedia
- **Mouse**: Poziționare absolută și relativă a mouse-ului
- **Audio**: Passthrough audio HDMI către difuzoarele uConsole

### **Funcționalități avansate**
- **Transfer de text**: Transferă rapid text prin simularea apăsărilor de taste—ideal pentru nume de utilizator, parole și fragmente de cod
- **USB comutabil**: Comută ușor accesul USB între uConsole și dispozitivul țintă folosind app-ul gazdă
