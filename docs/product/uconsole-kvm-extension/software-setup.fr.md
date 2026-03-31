---
title: "Configuration du logiciel"
description: "Guide complet de configuration logicielle pour l'extension KVM Openterface pour uConsole."
keywords: "installation Openterface, uConsole logiciel, configuration KVM, installation de l'application"
---

# **Configuration du logiciel** | Extension KVM Openterface pour uConsole

## Vue d'ensemble de l'installation

L'application Openterface permet à votre uConsole de fonctionner comme une interface KVM, vous permettant de contrôler des appareils cibles via l'écran, le clavier et le trackball intégrés.

!!! note "Exigences"
    - **uConsole** : nécessite l'application Openterface installée
    - **Cible** : aucune application requise — prend en charge Windows, macOS, Linux, Android, iOS
    - **Vidéo** : utilisez un câble HDMI standard. Avec un convertisseur HDMI alimenté, il prend également en charge des formats tels que **VGA** et **DP**. *Astuce : assurez-vous que le convertisseur est correctement alimenté, sinon vous pouvez obtenir un écran noir.*

    - **Backend vidéo recommandé** : Pour de meilleures performances et compatibilité avec les GPU arm64 (par ex. l'écosystème Raspberry Pi), utilisez **GStreamer** comme backend vidéo. Notez cependant que **Kali Linux** peut ne pas bien prendre en charge GStreamer.

## Méthodes d'installation

### **Option 1 : Téléchargement depuis GitHub Releases (Recommandé pour arm64)**

Téléchargez la dernière version de l'application Openterface pour **arm64** depuis notre [page GitHub Releases](https://github.com/TechxArtisanStudio/Openterface_QT/releases).

1. Rendez-vous sur la page [Openterface_QT Releases](https://github.com/TechxArtisanStudio/Openterface_QT/releases).
2. Téléchargez le paquet `.deb` le plus récent pour **arm64** (p. ex. `openterfaceqt_*_arm64.deb`).
3. Installez le paquet :
   ```bash
   sudo apt install ./openterfaceqt_*_arm64.deb
   ```
   *(Remplacez le nom du fichier par le nom réel si nécessaire.)*

---

### **Option 2 : Installation Flatpak**

Suivez notre [guide d'installation Flatpak](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md) pour les étapes détaillées.

---

### **Option 3 : Dépôt communautaire**

Si vous préférez la build communautaire maintenue par Rex :

1. **Ajouter le dépôt** :
    ```bash
    wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
    sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
    ```

2. **Installer le paquet** :
    ```bash
    sudo apt update
    sudo apt install openterfaceqt
    ```

!!! warning "Remarque sur le dépôt"
    Ces commandes nécessitent `sudo`. Le dépôt cible des paquets arm64 Bookworm ; vérifiez la compatibilité avec votre appareil avant d'installer.

## Rappels importants

!!! tip "Alimentation et première mise en route"
    - **Assurez-vous que votre uConsole est suffisamment chargée ou connectée à une source d'alimentation stable.** Une alimentation insuffisante peut entraîner un fonctionnement instable ou des problèmes de connexion.
    - **Si vous ne parvenez pas à contrôler l'appareil cible au premier essai :**
        1. Éteignez complètement la uConsole.
        2. Attendez au moins 10 secondes.
        3. Rallumez-la et réessayez.

!!! tip "Débit en bauds pour la communication série"
    - **Réglez le débit sur 9600 bauds** lors de l'utilisation de la communication série. Cela réduit le taux d'erreurs, car la uConsole ne fournit souvent pas assez de puissance pour maintenir 115200 de manière fiable.

## Instructions d'utilisation

### **Démarrer la session KVM**
1. Lancez l'application Openterface sur votre uConsole
2. L'application détectera automatiquement la carte d'extension KVM
3. Connectez votre appareil cible via HDMI
4. Utilisez le clavier et le trackball intégrés de la uConsole pour contrôler l'appareil

### **Fonctions de contrôle**
- **Clavier** : émulation complète du clavier, y compris les touches multimédias
- **Souris** : positionnement absolu et relatif de la souris
- **Audio** : passthrough audio HDMI vers les haut-parleurs de la uConsole

### **Fonctionnalités avancées**
- **Transfert de texte** : transmettez rapidement du texte en simulant des frappes — idéal pour les identifiants, mots de passe et extraits de code
- **USB commutable** : basculez facilement l'accès USB entre la uConsole et l'appareil cible via l'application hôte
---
title: "Configuration logicielle"
description: "Guide complet de configuration logicielle pour Openterface KVM Extension for uConsole. Apprenez comment installer et configurer l'App Openterface sur votre uConsole pour une fonctionnalité KVM transparente."
keywords: "installation app Openterface, configuration logicielle uConsole, configuration app KVM, configuration app uConsole, guide installation logicielle"
---

# **Configuration logicielle** | Openterface KVM Extension for uConsole

## Aperçu de l'installation

L'App Openterface permet à votre uConsole de fonctionner comme une interface KVM, vous permettant de contrôler les appareils cibles via l'écran intégré, le clavier et le trackball.

!!! note "Exigences"
    - **uConsole** : Nécessite l'installation de l'App Openterface
    - **Cible** : Aucune app nécessaire - prend en charge Windows, macOS, Linux, Android, iOS
    - **Vidéo** : Utilisez un câble HDMI standard. Utilisez un câble HDMI standard. Avec un convertisseur HDMI alimenté, il prend également en charge d'autres formats tels que **VGA**, **DP**, et plus. *Astuce : Assurez-vous que le convertisseur est correctement alimenté ; sinon, vous pourriez rencontrer un écran noir.*

## Méthodes d'installation

### **Option 1 : Installation Flatpak**

Suivez notre [Guide d'installation Flatpak](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md) pour les étapes de configuration détaillées.

### **Option 2 : Dépôt communautaire (Recommandé)**

Si vous préférez la build communautaire maintenue par Rex :

1. **Ajouter le dépôt** :
```bash
wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
```

2. **Installer le paquet** :
```bash
sudo apt update
sudo apt install openterfaceqt
```

!!! warning "Notes du dépôt"
    Ces commandes nécessitent sudo. Le dépôt cible les paquets arm64 Bookworm ; vérifiez la compatibilité avec votre appareil avant l'installation.

## Instructions d'utilisation

### **Démarrer la session KVM**
1. Lancez l'App Openterface sur votre uConsole
2. L'app détectera automatiquement la carte Extension KVM
3. Connectez votre appareil cible via HDMI
4. Utilisez le clavier et trackball intégrés du uConsole pour contrôler l'appareil cible

### **Fonctionnalités de contrôle**
- **Clavier** : Émulation complète du clavier incluant les touches multimédias
- **Souris** : Positionnement absolu et relatif de la souris
- **Audio** : Pass-through audio HDMI vers les haut-parleurs uConsole

### **Fonctionnalités avancées**
- **Transfert de texte** : Transmettez rapidement du texte en simulant des frappes—idéal pour les noms d'utilisateur, mots de passe et extraits de code
- **USB commutateur** : Basculez facilement l'accès USB entre le uConsole et l'appareil cible en utilisant l'app hôte
