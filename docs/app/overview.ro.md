# Software

Pentru a face funcționale gadget-urile Openterface™ KVM, va trebui să instalați una dintre aplicațiile enumerate mai jos pe computerul dvs. gazdă. Puteți descărca aceste aplicații de pe diferite platforme de aplicații sau pur și simplu să faceți clic pe linkurile furnizate. Dacă vă simțiți aventuroși, le puteți construi și din codul sursă folosind repository-urile noastre GitHub!

![use-case-pc-angled-view](https://assets.openterface.com/images/product/use-case-pc-angled-view.webp){ width=600 }

## Descărcare și Instalare

<div class="grid cards" markdown>

-   ### :fontawesome-brands-windows:{ .lg } **Windows**

    ***

    Descărcați sau construiți din codul sursă pentru **Openterface QT Win**:

    [:octicons-download-24: Descărcați Instalatorul {{qt_version}}](https://github.com/TechxArtisanStudio/Openterface_QT/releases/download/{{qt_version}}/openterfaceQT_windows_amd64_installer.exe) <br>
    [:octicons-download-24: Descărcați EXE Portabil {{qt_version}}](https://github.com/TechxArtisanStudio/Openterface_QT/releases/download/{{qt_version}}/openterfaceQT_windows_amd64_portable.exe) <br>
    [:octicons-mark-github-16: Openterface_QT](https://github.com/TechxArtisanStudio/Openterface_QT) <br>
    [:octicons-play-24: Urmăriți Demo](https://youtu.be/ERzpGtRvP2o?si=e9k402f0nxsD8o2j)

-   ### :fontawesome-brands-apple:{ .lg } **macOS**

    ***

    Descărcați sau construiți din codul sursă pentru **Openterface MacOS**:

    [:octicons-arrow-right-24: Instalați din App Store](/appstore) <br>
    [:octicons-download-24: Descărcați DMG Portabil](https://openterface.com/app/macos/dmg-installation/) <br>
    [:octicons-mark-github-16: Openterface_MacOS](https://github.com/TechxArtisanStudio/Openterface_MacOS) <br>
    [:octicons-play-24: Urmăriți Demo](https://youtu.be/m7OpUem0zqY?si=tclfl0Jl77tmE6_e)

-   ### :fontawesome-brands-linux:{ .lg } **Linux**

    ***

    Descărcați sau construiți din codul sursă pentru **Openterface QT Linux**:

    [:octicons-download-24: Descărcați {{qt_version}} AMD64 DEB](https://github.com/TechxArtisanStudio/Openterface_QT/releases/download/{{qt_version}}/openterfaceQT_linux_amd64.deb) <br>
    [:octicons-download-24: Descărcați {{qt_version}} AMD64 RPM](https://github.com/TechxArtisanStudio/Openterface_QT/releases/download/{{qt_version}}/openterfaceQT_linux_amd64.rpm) <br>
    [:octicons-download-24: Descărcați {{qt_version}} AMD64 AppImage](https://github.com/TechxArtisanStudio/Openterface_QT/releases/download/{{qt_version}}/openterfaceQT_linux_amd64.AppImage) <br>
    [:octicons-download-24: Descărcați {{qt_version}} ARM64 DEB](https://github.com/TechxArtisanStudio/Openterface_QT/releases/download/{{qt_version}}/openterfaceQT_linux_arm64.deb) <br>
    [:octicons-download-24: Descărcați {{qt_version}} ARM64 AppImage](https://github.com/TechxArtisanStudio/Openterface_QT/releases/download/{{qt_version}}/openterfaceQT_linux_arm64.AppImage) <br>
    [:octicons-mark-github-16: Openterface_QT](https://github.com/TechxArtisanStudio/Openterface_QT) <br>
    [:octicons-play-24: Urmăriți Demo](https://youtu.be/_ScpI6TC0Pk?si=FSg7A2zmST8QbFec)

-   ### :fontawesome-brands-android:{ .lg } **Android**

    ***

    Descărcați sau construiți din codul sursă pentru **Android APK**:

    [:octicons-arrow-right-24: Instalați din Google Play](https://play.google.com/store/apps/details?id=com.openterface.AOS)<br>
    [:octicons-download-24: Descărcați {{android_version}}](https://github.com/TechxArtisanStudio/Openterface_Android/releases/download/{{android_version}}/OpenterfaceAndroid-release.apk) <br>
    [:octicons-mark-github-16: Openterface_Android](https://github.com/TechxArtisanStudio/Openterface_Android) <br>
    [:octicons-play-24: Urmăriți Demo](https://x.com/TechxArtisan/status/1825460088922071398)

</div>

???+ warning "Atenție: Verificați Confidențialitatea și Securitatea cu Aplicațiile Terțe"
Deoarece toate aplicațiile noastre sunt open source, s-ar putea să întâlniți versiuni alternative de aplicații gazdă pentru dispozitivele Openterface create de alții. Acestea pot fi destul de cool și pot oferi funcții suplimentare, dar iată o reamintire prietenoasă: examinați cu atenție practicile lor de securitate și confidențialitate—mai ales pentru că controlul KVM implică evenimente de pe ecranul, tastatura și mouse-ul dvs. Echipa Openterface nu poate garanta siguranța acestor aplicații terțe, așa că procedați cu prudență!

## Controale de Bază ale Aplicației Gazdă

### 💻 Compatibilitate

-   **Software Gazdă**: Instalați aplicația noastră gazdă pentru macOS, Windows sau Linux.
-   **Dispozitive Țintă**: Nu este necesară nicio configurare—doar conectați orice dispozitiv cu ieșire video (HDMI, VGA, etc.) și o portă USB pentru controlul tastaturii/mouse-ului. Funcționează cu Windows, macOS, Linux, Android și iOS.

### 🖱 Moduri Mouse

-   **Modul Absolut**: Mouse-ul gazdă mapează direct la poziția ecranului țintă.
-   **Modul Relativ**: Mișcă cursorul țintă relativ la poziția curentă. Ieșiți cu o comandă rapidă.

### ⌨️ Tastatură

Tastele apăsate de pe gazdă sunt trimise direct la țintă când aplicația este focalizată.

### ⚙️ Acces BIOS

Controlați direct BIOS-ul țintă.  
Taste comune: F2 (Dell/Lenovo/ASUS), F10 (HP), Del (ASUS/Gigabyte/MSI), ⌥ (Apple).

### 🔊 Audio

Audio-ul țintă se transmite prin HDMI și se redă pe computerul dvs. gazdă.

### 🎥 Video

Vizualizați ecranul dvs. țintă direct în aplicație.

-   **Modele Actuale**: Afișare de până la **1080p 30Hz** în aplicație, cu suport pentru intrare **4K 30Hz** prin HDMI.
-   **Alte Intrări**: Compatibil cu VGA, DVI, Micro HDMI și mai multe când folosiți adaptoare potrivite.
-   **Modele Viitoare**: Rezoluții și rate de cadre mai mari vor fi suportate pe măsură ce vor fi lansate noi versiuni de hardware.

### 🔄 Porturi Comutabile

Unele dispozitive Openterface includ porturi care pot fi **comutate între gazdă și țintă**, cum ar fi porturile USB 2.0 sau sloturile pentru carduri micro-SD (pe modelele viitoare).

-   **Folosirea Unul câte Unul**: Doar o parte (gazdă sau țintă) poate accesa portul la un moment dat.
-   **Metode de Comutare**:
    -   **Comutator Hardware** — comutator fizic pe dispozitiv
    -   **Buton Software** — control prin aplicația gazdă
-   **Important**:
    -   Ejectați în siguranță dispozitivele de stocare (drive-uri USB sau carduri micro-SD) înainte de comutare.
    -   Evitați conectarea dispozitivelor de înaltă putere pentru a preveni instabilitatea sau deteriorarea.
    -   Vedeți [Ghidul pentru Porturi Comutabile](/usb-switch) pentru detalii și diagrame logice.


## Actualizări

<!-- AUTO-GENERATED: This section is automatically generated by scripts/update-post-tool/generate_app_overview_updates.py -->
<!-- DO NOT EDIT MANUALLY -->

- Feb 03, 2026: [Sfat Copiere/Lipire Ubuntu (macOS → Ubuntu)](updates/20260203-macos-ubuntu-copy-paste.ro.md)
- Dec 18, 2025: [Viteza mouse-ului și performanța în jocuri a Openterface Mini-KVM pe macOS](updates/20251218-macos-mouse-speed.ro.md)

[:octicons-arrow-right-24: Citește mai multe actualizări](/app/updates)

<!-- END AUTO-GENERATED -->

