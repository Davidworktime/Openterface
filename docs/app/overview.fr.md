# Logiciel

Pour faire fonctionner vos gadgets Openterface™ KVM, vous devrez installer l'une des applications listées ci-dessous sur votre ordinateur hôte. Vous pouvez récupérer ces applications depuis différentes plateformes d'applications ou simplement cliquer sur les liens fournis. Si vous vous sentez aventureux, vous pouvez également les construire à partir du code source en utilisant nos dépôts GitHub !

![use-case-pc-angled-view](https://assets.openterface.com/images/product/use-case-pc-angled-view.webp){ width=600 }

## Téléchargement et Installation

<div class="grid cards" markdown>

-   ### :fontawesome-brands-windows:{ .lg } **Windows**

    ***

    Télécharger ou construire depuis le code source pour **Openterface QT Win** :

    [:octicons-download-24: Télécharger l'installateur {{qt_version}}](https://github.com/TechxArtisanStudio/Openterface_QT/releases/download/{{qt_version}}/openterfaceQT_windows_amd64_installer.exe) <br>
    [:octicons-download-24: Télécharger l'EXE portable {{qt_version}}](https://github.com/TechxArtisanStudio/Openterface_QT/releases/download/{{qt_version}}/openterfaceQT_windows_amd64_portable.exe) <br>
    [:octicons-mark-github-16: Openterface_QT](https://github.com/TechxArtisanStudio/Openterface_QT) <br>
    [:octicons-play-24: Regarder la démo](https://youtu.be/ERzpGtRvP2o?si=e9k402f0nxsD8o2j)

-   ### :fontawesome-brands-apple:{ .lg } **macOS**

    ***

    Télécharger ou construire depuis le code source pour **Openterface MacOS** :

    [:octicons-arrow-right-24: Installer depuis l'App Store](/appstore) <br>
    [:octicons-download-24: Télécharger le DMG portable](https://openterface.com/app/macos/dmg-installation/) <br>
    [:octicons-mark-github-16: Openterface_MacOS](https://github.com/TechxArtisanStudio/Openterface_MacOS) <br>
    [:octicons-play-24: Regarder la démo](https://youtu.be/m7OpUem0zqY?si=tclfl0Jl77tmE6_e)

-   ### :fontawesome-brands-linux:{ .lg } **Linux**

    ***

    Télécharger ou construire depuis le code source pour **Openterface QT Linux** :

    [:octicons-download-24: Télécharger {{qt_version}} AMD64 DEB](https://github.com/TechxArtisanStudio/Openterface_QT/releases/download/{{qt_version}}/openterfaceQT_linux_amd64.deb) <br>
    [:octicons-download-24: Télécharger {{qt_version}} AMD64 RPM](https://github.com/TechxArtisanStudio/Openterface_QT/releases/download/{{qt_version}}/openterfaceQT_linux_amd64.rpm) <br>
    [:octicons-download-24: Télécharger {{qt_version}} AMD64 AppImage](https://github.com/TechxArtisanStudio/Openterface_QT/releases/download/{{qt_version}}/openterfaceQT_linux_amd64.AppImage) <br>
    [:octicons-download-24: Télécharger {{qt_version}} ARM64 DEB](https://github.com/TechxArtisanStudio/Openterface_QT/releases/download/{{qt_version}}/openterfaceQT_linux_arm64.deb) <br>
    [:octicons-download-24: Télécharger {{qt_version}} ARM64 AppImage](https://github.com/TechxArtisanStudio/Openterface_QT/releases/download/{{qt_version}}/openterfaceQT_linux_arm64.AppImage) <br>
    [:octicons-mark-github-16: Openterface_QT](https://github.com/TechxArtisanStudio/Openterface_QT) <br>
    [:octicons-play-24: Regarder la démo](https://youtu.be/_ScpI6TC0Pk?si=FSg7A2zmST8QbFec)

-   ### :fontawesome-brands-android:{ .lg } **Android**

    ***

    Télécharger ou construire depuis le code source pour **Android APK** :

    [:octicons-arrow-right-24: Installer depuis le Google Play Store](https://play.google.com/store/apps/details?id=com.openterface.AOS)<br>
    [:octicons-download-24: Télécharger {{android_version}}](https://github.com/TechxArtisanStudio/Openterface_Android/releases/download/{{android_version}}/OpenterfaceAndroid-release.apk) <br>
    [:octicons-mark-github-16: Openterface_Android](https://github.com/TechxArtisanStudio/Openterface_Android) <br>
    [:octicons-play-24: Regarder la démo](https://x.com/TechxArtisan/status/1825460088922071398)

</div>

???+ warning "Attention : Vérifiez la confidentialité et la sécurité des applications tierces"
Comme toutes nos applications sont open source, vous pourriez tomber sur des versions alternatives d'applications hôtes pour les appareils Openterface créées par d'autres. Elles peuvent être assez cool et offrir des fonctionnalités supplémentaires, mais voici un rappel amical : examinez attentivement leurs pratiques de sécurité et de confidentialité—surtout parce que le contrôle KVM implique des événements de votre écran, clavier et souris. L'équipe Openterface ne peut pas garantir la sécurité de ces applications tierces, alors procédez avec prudence !

## Contrôles de base de l'application hôte

### 💻 Compatibilité

-   **Logiciel hôte** : Installez notre application hôte pour macOS, Windows ou Linux.
-   **Appareils cibles** : Aucune configuration nécessaire—connectez simplement n'importe quel appareil avec une sortie vidéo (HDMI, VGA, etc.) et un port USB pour le contrôle clavier/souris. Fonctionne avec Windows, macOS, Linux, Android et iOS.

### 🖱 Modes de souris

-   **Mode absolu** : La souris hôte mappe directement à la position de l'écran cible.
-   **Mode relatif** : Déplace le curseur cible par rapport à la position actuelle. Sortez avec un raccourci.

### ⌨️ Clavier

Les frappes de touches de l'hôte sont envoyées directement à la cible lorsque l'application est focalisée.

### ⚙️ Accès BIOS

Contrôlez directement le BIOS cible.  
Touches communes : F2 (Dell/Lenovo/ASUS), F10 (HP), Del (ASUS/Gigabyte/MSI), ⌥ (Apple).

### 🔊 Audio

L'audio cible diffuse via HDMI et se joue sur votre ordinateur hôte.

### 🎥 Vidéo

Visualisez votre écran cible directement dans l'application.

-   **Modèles actuels** : Affichage jusqu'à **1080p 30Hz** dans l'application, avec support pour l'entrée **4K 30Hz** via HDMI.
-   **Autres entrées** : Compatible avec VGA, DVI, Micro HDMI et plus lors de l'utilisation d'adaptateurs appropriés.
-   **Modèles futurs** : Des résolutions et taux de rafraîchissement plus élevés seront supportés au fur et à mesure que de nouvelles versions matérielles seront publiées.

### 🔄 Ports commutables

Certains appareils Openterface incluent des ports qui peuvent être **commutés entre l'hôte et la cible**, tels que les ports USB 2.0 ou les emplacements de cartes micro-SD (sur les modèles à venir).

-   **Utilisation une à la fois** : Un seul côté (hôte ou cible) peut accéder au port à la fois.
-   **Méthodes de commutation** :
    -   **Basculement matériel** — commutateur physique sur l'appareil
    -   **Bouton logiciel** — contrôle via l'application hôte
-   **Important** :
    -   Éjectez en toute sécurité les dispositifs de stockage (disques USB ou cartes micro-SD) avant de commuter.
    -   Évitez de connecter des dispositifs haute puissance pour prévenir l'instabilité ou les dommages.
    -   Voir le [Guide des ports commutables](/usb-switch) pour les détails et les diagrammes logiques.


## Actualités

<!-- AUTO-GENERATED: This section is automatically generated by scripts/update-post-tool/generate_app_overview_updates.py -->
<!-- DO NOT EDIT MANUALLY -->

- Feb 03, 2026: [Astuce Copier/Coller Ubuntu (macOS → Ubuntu)](updates/20260203-macos-ubuntu-copy-paste.fr.md)
- Dec 18, 2025: [Vitesse de souris et performances de jeu Openterface Mini-KVM sur macOS](updates/20251218-macos-mouse-speed.fr.md)

[:octicons-arrow-right-24: Lire plus d'actualités](/app/updates)

<!-- END AUTO-GENERATED -->

