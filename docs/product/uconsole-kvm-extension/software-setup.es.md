---
title: "Configuración de Software"
description: "Guía completa de configuración del software para la extensión KVM Openterface en uConsole."
keywords: "instalación Openterface, uConsole software, configuración KVM, instalación de la app"
---

# **Configuración de Software** | Extensión KVM Openterface para uConsole

## Resumen de instalación

La aplicación Openterface permite que su uConsole funcione como una interfaz KVM, permitiéndole controlar dispositivos objetivo mediante la pantalla, el teclado y el trackball integrados.

!!! note "Requisitos"
    - **uConsole**: Requiere la aplicación Openterface instalada
    - **Dispositivo objetivo**: No necesita aplicación — compatible con Windows, macOS, Linux, Android, iOS
    - **Vídeo**: Use un cable HDMI estándar. Con un convertidor HDMI con alimentación, también soporta formatos como **VGA** y **DP**. *Consejo: Asegúrese de que el convertidor tenga la alimentación adecuada; de lo contrario, puede aparecer una pantalla negra.*

    - **Backend de vídeo recomendado**: Para mejor rendimiento y compatibilidad con GPUs arm64 (por ejemplo, Raspberry Pi), use **GStreamer** como backend de vídeo. Tenga en cuenta que **Kali Linux** puede no soportar bien GStreamer.

## Métodos de instalación

### **Opción 1: Descargar desde GitHub Releases (Recomendado para arm64)**

Descargue la última versión de la aplicación Openterface para **arm64** directamente desde nuestra [página de Releases en GitHub](https://github.com/TechxArtisanStudio/Openterface_QT/releases).

1. Visite la página [Openterface_QT Releases](https://github.com/TechxArtisanStudio/Openterface_QT/releases).
2. Descargue el paquete `.deb` más reciente para **arm64** (p.ej., `openterfaceqt_*_arm64.deb`).
3. Instale el paquete:
   ```bash
   sudo apt install ./openterfaceqt_*_arm64.deb
   ```
   *(Reemplace el nombre de archivo según corresponda.)*

---

### **Opción 2: Instalación Flatpak**

Siga nuestra [Guía de instalación Flatpak](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md) para pasos detallados.

---

### **Opción 3: Repositorio de la comunidad**

Si prefiere la compilación comunitaria mantenida por Rex:

1. **Añadir repositorio**:
    ```bash
    wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
    sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
    ```

2. **Instalar paquete**:
    ```bash
    sudo apt update
    sudo apt install openterfaceqt
    ```

!!! warning "Notas del repositorio"
    Estos comandos requieren `sudo`. El repositorio está dirigido a paquetes arm64 Bookworm; verifique la compatibilidad con su dispositivo antes de instalar.

## Recordatorios importantes

!!! tip "Alimentación y primera configuración"
    - **Asegúrese de que su uConsole esté suficientemente cargada o conectada a una fuente de alimentación estable.** La baja potencia puede causar un funcionamiento inestable o problemas de conexión.
    - **Si no puede controlar el dispositivo objetivo en el primer intento:**
        1. Apague completamente la uConsole.
        2. Espere al menos 10 segundos.
        3. Enciéndala de nuevo e intente otra vez.

!!! tip "Baudios de comunicación serial"
    - **Configure la velocidad en 9600 baudios** para la comunicación serial. Esto reduce la tasa de errores, ya que la uConsole a menudo no puede suministrar suficiente energía para mantener 115200 de forma fiable.

## Instrucciones de uso

### **Iniciar la sesión KVM**
1. Abra la aplicación Openterface en su uConsole
2. La aplicación detectará automáticamente la placa de extensión KVM
3. Conecte su dispositivo objetivo por HDMI
4. Use el teclado y el trackball integrados de la uConsole para controlar el dispositivo

### **Funciones de control**
- **Teclado**: Emulación completa del teclado, incluidas teclas multimedia
- **Ratón**: Posicionamiento absoluto y relativo del ratón
- **Audio**: Redirección de audio HDMI a los altavoces de la uConsole

### **Funciones avanzadas**
- **Transferencia de texto**: Envíe texto simulando pulsaciones — ideal para nombres de usuario, contraseñas y fragmentos de código
- **USB conmutables**: Cambie el acceso USB entre la uConsole y el dispositivo objetivo mediante la app host
---
title: "Configuración de software"
description: "Guía completa de configuración de software para Openterface KVM Extension for uConsole. Aprende cómo instalar y configurar la App Openterface en tu uConsole para funcionalidad KVM sin problemas."
keywords: "instalación app Openterface, configuración software uConsole, configuración app KVM, configuración app uConsole, guía instalación software"
---

# **Configuración de software** | Openterface KVM Extension for uConsole

## Resumen de instalación

La App Openterface permite que tu uConsole funcione como una interfaz KVM, permitiéndote controlar dispositivos objetivo a través de la pantalla integrada, teclado y trackball.

!!! note "Requisitos"
    - **uConsole**: Requiere instalación de la App Openterface
    - **Objetivo**: No se necesita app - soporta Windows, macOS, Linux, Android, iOS
    - **Video**: Usa un cable HDMI estándar. Usa un cable HDMI estándar. Con un convertidor HDMI alimentado, también soporta otros formatos como **VGA**, **DP** y más. *Consejo: Asegúrate de que el convertidor esté correctamente alimentado; de lo contrario, puedes experimentar una pantalla negra.*

## Métodos de instalación

### **Opción 1: Instalación Flatpak**

Sigue nuestra [Guía de instalación Flatpak](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md) para pasos de configuración detallados.

### **Opción 2: Repositorio de la comunidad (Recomendado)**

Si prefieres la build de la comunidad mantenida por Rex:

1. **Añadir repositorio**:
```bash
wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
```

2. **Instalar paquete**:
```bash
sudo apt update
sudo apt install openterfaceqt
```

!!! warning "Notas del repositorio"
    Estos comandos requieren sudo. El repositorio está dirigido a paquetes arm64 Bookworm; verifica la compatibilidad con tu dispositivo antes de instalar.

## Instrucciones de uso

### **Iniciar sesión KVM**
1. Lanza la App Openterface en tu uConsole
2. La app detectará automáticamente la placa Extension KVM
3. Conecta tu dispositivo objetivo vía HDMI
4. Usa el teclado y trackball integrados del uConsole para controlar el dispositivo objetivo

### **Características de control**
- **Teclado**: Emulación completa del teclado incluyendo teclas multimedia
- **Ratón**: Posicionamiento absoluto y relativo del ratón
- **Audio**: Passthrough de audio HDMI a los altavoces del uConsole

### **Características avanzadas**
- **Transferencia de texto**: Transfiere rápidamente texto simulando pulsaciones de teclas—ideal para nombres de usuario, contraseñas y fragmentos de código
- **USB conmutable**: Cambia fácilmente el acceso USB entre el uConsole y el dispositivo objetivo usando la app anfitrión
