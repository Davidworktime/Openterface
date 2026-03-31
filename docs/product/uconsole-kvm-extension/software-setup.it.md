---
title: "Configurazione del software"
description: "Guida completa alla configurazione del software per l'estensione KVM Openterface per uConsole."
keywords: "installazione Openterface, uConsole software, configurazione KVM, installazione app"
---

# **Configurazione del software** | Estensione KVM Openterface per uConsole

## Panoramica installazione

L'app Openterface consente alla tua uConsole di funzionare come un'interfaccia KVM, permettendoti di controllare dispositivi target tramite lo schermo integrato, la tastiera e il trackball.

!!! note "Requisiti"
    - **uConsole**: Richiede l'app Openterface installata
    - **Target**: Nessuna app necessaria — supporta Windows, macOS, Linux, Android, iOS
    - **Video**: Usa un cavo HDMI standard. Con un convertitore HDMI alimentato, supporta anche formati come **VGA** e **DP**. *Suggerimento: assicurati che il convertitore sia correttamente alimentato, altrimenti potresti avere uno schermo nero.*

    - **Backend video consigliato**: Per le migliori prestazioni e compatibilità con GPU arm64 (es. ecosistema Raspberry Pi), usa **GStreamer** come backend video. Nota che **Kali Linux** potrebbe non supportare bene GStreamer.

## Metodi di installazione

### **Opzione 1: Download da GitHub Releases (Consigliato per arm64)**

Scarica l'ultima release dell'App Openterface per **arm64** direttamente dalla nostra [pagina Releases di GitHub](https://github.com/TechxArtisanStudio/Openterface_QT/releases).

1. Visita la pagina [Openterface_QT Releases](https://github.com/TechxArtisanStudio/Openterface_QT/releases).
2. Scarica il pacchetto `.deb` più recente per **arm64** (es. `openterfaceqt_*_arm64.deb`).
3. Installa il pacchetto:
   ```bash
   sudo apt install ./openterfaceqt_*_arm64.deb
   ```
   *(Sostituisci il nome del file con quello reale se diverso.)*

---

### **Opzione 2: Installazione Flatpak**

Segui la nostra [Guida all'installazione Flatpak](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md) per i passaggi dettagliati.

---

### **Opzione 3: Repository della community**

Se preferisci la build community mantenuta da Rex:

1. **Aggiungi il repository**:
    ```bash
    wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
    sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
    ```

2. **Installa il pacchetto**:
    ```bash
    sudo apt update
    sudo apt install openterfaceqt
    ```

!!! warning "Note sul repository"
    Questi comandi richiedono `sudo`. Il repository è destinato a pacchetti arm64 Bookworm; verifica la compatibilità con il tuo dispositivo prima di installare.

## Promemoria importanti

!!! tip "Alimentazione e primo avvio"
    - **Assicurati che la tua uConsole sia sufficientemente carica o collegata a una fonte di alimentazione stabile.** La bassa alimentazione può causare funzionamento instabile o problemi di connessione.
    - **Se non riesci a controllare il dispositivo target al primo tentativo:**
        1. Spegni completamente la uConsole.
        2. Attendi almeno 10 secondi.
        3. Riaccendila e riprova.

!!! tip "Baudrate comunicazione seriale"
    - **Imposta il baudrate su 9600** durante l'uso della comunicazione seriale. Questo riduce il tasso di errore, poiché la uConsole spesso non fornisce abbastanza potenza per mantenere 115200 in modo affidabile.

## Istruzioni d'uso

### **Avviare la sessione KVM**
1. Avvia l'app Openterface sulla tua uConsole
2. L'app rileverà automaticamente la scheda di estensione KVM
3. Collega il dispositivo target via HDMI
4. Usa la tastiera e il trackball integrati per controllare il dispositivo

### **Funzionalità di controllo**
- **Tastiera**: Emulazione completa della tastiera, incluse le tastiere multimediali
- **Mouse**: Posizionamento assoluto e relativo del mouse
- **Audio**: Passaggio audio HDMI agli altoparlanti della uConsole

### **Funzionalità avanzate**
- **Trasferimento testo**: Trasmetti rapidamente testo simulando battiture — ideale per nomi utente, password e snippet di codice
- **USB commutabile**: Cambia facilmente l'accesso USB tra la uConsole e il dispositivo target tramite l'app host
---
title: "Configurazione software"
description: "Guida completa alla configurazione software per Openterface KVM Extension for uConsole. Impara come installare e configurare l'App Openterface sul tuo uConsole per funzionalità KVM senza interruzioni."
keywords: "installazione app Openterface, configurazione software uConsole, configurazione app KVM, configurazione app uConsole, guida installazione software"
---

# **Configurazione software** | Openterface KVM Extension for uConsole

## Panoramica installazione

L'App Openterface consente al tuo uConsole di funzionare come un'interfaccia KVM, permettendoti di controllare i dispositivi target attraverso lo schermo integrato, la tastiera e il trackball.

!!! note "Requisiti"
    - **uConsole**: Richiede l'installazione dell'App Openterface
    - **Target**: Nessuna app necessaria - supporta Windows, macOS, Linux, Android, iOS
    - **Video**: Usa un cavo HDMI standard. Usa un cavo HDMI standard. Con un convertitore HDMI alimentato, supporta anche altri formati come **VGA**, **DP** e altro. *Suggerimento: Assicurati che il convertitore sia correttamente alimentato; altrimenti potresti riscontrare uno schermo nero.*

## Metodi di installazione

### **Opzione 1: Installazione Flatpak**

Segui la nostra [Guida all'installazione Flatpak](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md) per i passaggi di configurazione dettagliati.

### **Opzione 2: Repository della comunità (Raccomandato)**

Se preferisci la build della comunità mantenuta da Rex:

1. **Aggiungi Repository**:
```bash
wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
```

2. **Installa Pacchetto**:
```bash
sudo apt update
sudo apt install openterfaceqt
```

!!! warning "Note Repository"
    Questi comandi richiedono sudo. Il repository è rivolto ai pacchetti arm64 Bookworm; verifica la compatibilità con il tuo dispositivo prima dell'installazione.

## Istruzioni per l'uso

### **Avvio sessione KVM**
1. Avvia l'App Openterface sul tuo uConsole
2. L'app rileverà automaticamente la scheda Extension KVM
3. Collega il tuo dispositivo target tramite HDMI
4. Usa la tastiera e trackball integrati del uConsole per controllare il dispositivo target

### **Funzionalità di controllo**
- **Tastiera**: Emulazione completa della tastiera inclusi i tasti multimediali
- **Mouse**: Posizionamento assoluto e relativo del mouse
- **Audio**: Pass-through audio HDMI agli altoparlanti uConsole

### **Funzionalità avanzate**
- **Trasferimento testo**: Trasferisci rapidamente testo simulando pressioni di tasti—ideale per nomi utente, password e frammenti di codice
- **USB commutabile**: Commuta facilmente l'accesso USB tra uConsole e dispositivo target usando l'app host
