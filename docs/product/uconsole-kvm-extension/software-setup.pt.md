---
title: "Configuração de Software"
description: "Guia completo de configuração de software para a extensão KVM Openterface para uConsole."
keywords: "instalação Openterface, software uConsole, configuração KVM, instalação do app"
---

# **Configuração de Software** | Extensão KVM Openterface para uConsole

## Visão geral da instalação

O aplicativo Openterface permite que sua uConsole funcione como uma interface KVM, permitindo controlar dispositivos alvo através da tela, teclado e trackball integrados.

!!! note "Requisitos"
    - **uConsole**: Requer o aplicativo Openterface instalado
    - **Alvo**: Nenhum app necessário — suporta Windows, macOS, Linux, Android, iOS
    - **Vídeo**: Use um cabo HDMI padrão. Com um conversor HDMI alimentado, também suporta formatos como **VGA** e **DP**. *Dica: verifique se o conversor está devidamente alimentado; caso contrário, pode ocorrer tela preta.*

    - **Backend de vídeo recomendado**: Para melhor desempenho e compatibilidade com GPUs arm64 (por exemplo, Raspberry Pi), use **GStreamer** como backend de vídeo. Note que **Kali Linux** pode não suportar bem o GStreamer.

## Métodos de instalação

### **Opção 1: Download do GitHub Releases (Recomendado para arm64)**

Faça o download da versão mais recente do aplicativo Openterface para **arm64** diretamente em nossa [página de Releases no GitHub](https://github.com/TechxArtisanStudio/Openterface_QT/releases).

1. Visite a página [Openterface_QT Releases](https://github.com/TechxArtisanStudio/Openterface_QT/releases).
2. Baixe o pacote `.deb` mais recente para **arm64** (por exemplo, `openterfaceqt_*_arm64.deb`).
3. Instale o pacote:
   ```bash
   sudo apt install ./openterfaceqt_*_arm64.deb
   ```
   *(Substitua o nome do arquivo, se for diferente.)*

---

### **Opção 2: Instalação via Flatpak**

Siga nosso [Guia de Instalação Flatpak](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md) para instruções detalhadas.

---

### **Opção 3: Repositório da comunidade**

Se preferir a build mantida pela comunidade (Rex):

1. **Adicionar repositório**:
    ```bash
    wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
    sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
    ```

2. **Instalar pacote**:
    ```bash
    sudo apt update
    sudo apt install openterfaceqt
    ```

!!! warning "Notas sobre o repositório"
    Estes comandos requerem `sudo`. O repositório é voltado a pacotes arm64 Bookworm; verifique a compatibilidade com seu dispositivo antes de instalar.

## Lembretes importantes

!!! tip "Energia & Primeira Inicialização"
    - **Certifique-se de que sua uConsole esteja suficientemente carregada ou conectada a uma fonte de energia estável.** Baixa energia pode causar operação instável ou problemas de conexão.
    - **Se não conseguir controlar o dispositivo alvo na primeira tentativa:**
        1. Desligue completamente a uConsole.
        2. Aguarde pelo menos 10 segundos.
        3. Ligue novamente e tente de novo.

!!! tip "Baudrate de comunicação serial"
    - **Configure o baudrate para 9600** ao usar comunicação serial. Isso reduz a taxa de erro, pois a uConsole frequentemente não fornece energia suficiente para manter 115200 de forma confiável.

## Instruções de uso

### **Iniciar sessão KVM**
1. Inicie o aplicativo Openterface na sua uConsole
2. O aplicativo detectará automaticamente a placa de extensão KVM
3. Conecte o dispositivo alvo via HDMI
4. Use o teclado e o trackball integrados para controlar o dispositivo

### **Recursos de controle**
- **Teclado**: Emulação completa de teclado incluindo teclas multimídia
- **Mouse**: Posicionamento absoluto e relativo do mouse
- **Áudio**: Passagem de áudio HDMI para os alto-falantes da uConsole

### **Recursos avançados**
- **Transferência de texto**: Transfira rapidamente texto simulando pressionamentos de tecla — ideal para nomes de usuário, senhas e trechos de código
- **USB comutável**: Alterne o acesso USB entre a uConsole e o dispositivo alvo usando o app host
---
title: "Configuração de software"
description: "Guia completo de configuração de software para Openterface KVM Extension for uConsole. Aprenda como instalar e configurar o App Openterface no seu uConsole para funcionalidade KVM perfeita."
keywords: "instalação app Openterface, configuração software uConsole, configuração app KVM, configuração app uConsole, guia instalação software"
---

# **Configuração de software** | Openterface KVM Extension for uConsole

## Visão geral da instalação

O App Openterface permite que seu uConsole funcione como uma interface KVM, permitindo que você controle dispositivos alvo através da tela integrada, teclado e trackball.

!!! note "Requisitos"
    - **uConsole**: Requer instalação do App Openterface
    - **Alvo**: Nenhum app necessário - suporta Windows, macOS, Linux, Android, iOS
    - **Vídeo**: Use um cabo HDMI padrão. Use um cabo HDMI padrão. Com um conversor HDMI alimentado, também suporta outros formatos como **VGA**, **DP** e mais. *Dica: Certifique-se de que o conversor esteja adequadamente alimentado; caso contrário, você pode experimentar uma tela preta.*

## Métodos de instalação

### **Opção 1: Instalação Flatpak**

Siga nosso [Guia de instalação Flatpak](https://github.com/TechxArtisanStudio/Openterface_QT/blob/main/docs/flatpak_installation.md) para etapas de configuração detalhadas.

### **Opção 2: Repositório da comunidade (Recomendado)**

Se você prefere a build da comunidade mantida pelo Rex:

1. **Adicionar repositório**:
```bash
wget -q -O- https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm/KEY.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/ak-rex.gpg
sudo add-apt-repository -y "deb [arch=arm64] https://raw.githubusercontent.com/ak-rex/ClockworkPi-apt/main/bookworm stable main"
```

2. **Instalar pacote**:
```bash
sudo apt update
sudo apt install openterfaceqt
```

!!! warning "Notas do repositório"
    Esses comandos requerem sudo. O repositório visa pacotes arm64 Bookworm; verifique a compatibilidade com seu dispositivo antes de instalar.

## Instruções de uso

### **Iniciar sessão KVM**
1. Lance o App Openterface no seu uConsole
2. O app detectará automaticamente a placa Extension KVM
3. Conecte seu dispositivo alvo via HDMI
4. Use o teclado e trackball integrados do uConsole para controlar o dispositivo alvo

### **Recursos de controle**
- **Teclado**: Emulação completa do teclado incluindo teclas multimídia
- **Mouse**: Posicionamento absoluto e relativo do mouse
- **Áudio**: Pass-through de áudio HDMI para os alto-falantes do uConsole

### **Recursos avançados**
- **Transferência de texto**: Transfira rapidamente texto simulando pressionamentos de teclas—ideal para nomes de usuário, senhas e trechos de código
- **USB comutável**: Mude facilmente o acesso USB entre uConsole e dispositivo alvo usando o app host
