---
draft: false
date: 2026-03-05
title: "Correção térmica DP/VGA KVM-GO – Registro de engenharia"
description: "Análise detalhada do problema de calor DP e VGA no KVM-GO: medições, alterações PCB e correções mecânicas que resolveram o sobreaquecimento sem adicionar ventilador."
keywords: "correção térmica KVM-GO, calor DP, calor VGA, KVM-over-USB engenharia, layout PCB, gestão térmica, Openterface, registro engenharia"
author: "TechxArtisan Studio"
category: "Atualizações de produto"
tags: ["KVM-GO", "Térmico", "Registro engenharia", "Design de produto"]
featured: false
social:
  image: "https://assets.openterface.com/images/kvm-go/thermal-fix.webp"
  title: "Resolução do calor DP/VGA no KVM-GO"
  description: "Como corrigimos o sobreaquecimento das variantes DP e VGA do KVM-GO através de melhorias de layout e condução."
---

# Registro de engenharia: Rastreando o calor DP/VGA no KVM-GO (e a correção que finalmente funcionou)

## Entrada 1: O momento em que percebemos que não era um “calor normal”
A meio do desenvolvimento do KVM-GO, observámos um comportamento térmico que não correspondia às expectativas típicas de “pequeno dispositivo que aquece”. O problema surgia apenas em duas variantes: DisplayPort (DP) e VGA. A variante HDMI mantinha-se dentro do esperado.

No início o sintoma era simples: a temperatura do invólucro tornava-se incómoda mais cedo do que o previsto. O que nos preocupava não era o conforto, mas a possibilidade de as temperaturas internas estarem muito acima do que os componentes de consumo estão concebidos para tolerar ao longo do tempo.


---

## Entrada 2: Por que só DP e VGA
Após rastrear o design do caminho de vídeo entre versões, surgiu um padrão.

- HDMI: um único estádio de conversão (HDMI para vídeo USB) usando MS2130S
- DP: cadeia de dois chips (IT6563 mais MS2130S) para converter DP em vídeo USB
- VGA: cadeia de dois chips (MS9288C mais MS2109S) para converter VGA em vídeo USB

Dois chips não acrescentam apenas componentes. Acrescentam dissipação de potência e pontos quentes localizados. Num produto do tamanho do KVM-GO, esses pontos quentes têm muito pouco espaço para se espalhar.

Depois deparámos com a segunda restrição: a área superficial. O KVM-GO leva o tamanho ao limite, o que significa que a área de PCB e a área efetiva de dissipação térmica são ambas minúsculas.

Por fim, havia uma restrição de layout que se tornou um verdadeiro compromisso de engenharia. Colocar os dois chips quentes no mesmo lado parece ideal termicamente, mas os requisitos de pinout e roteamento de alta velocidade tornaram essa abordagem difícil. Colocar um chip mais “interior” simplificava o roteamento e ajudava à integridade do sinal, mas prendia o calor no interior do invólucro.

![Original-PCB-layout](https://assets2.openterface.com/images/Original-PCB-layout.webp)

*Layout PCB original*

![original-Wiring](https://assets2.openterface.com/images/original-Wiring.webp)

*Roteamento de alta velocidade original*

![KVM-Go-tructure](https://assets2.openterface.com/images/KVM-Go-tructure.webp)


*Estrutura interna de empilhamento KVM-GO*

---

## Entrada 3: Medir o que importa, temperatura interna vs externa
Decidimos parar de adivinhar e medir ambos os lados do problema. Criámos pontos de medição de temperatura para monitorização externa e interna e executámos um teste de carga prolongada.

O resultado foi alarmante, especialmente no VGA.

Após aproximadamente uma hora de funcionamento sustentado:
- a superfície externa atingiu cerca de 65 °C
- a temperatura interna atingiu picos em torno de 115 °C

Muitos componentes de consumo estão especificados para temperaturas operacionais máximas em torno de 85 °C, dependendo da peça e grau exatos. Ver temperaturas internas de três dígitos significava que não estávamos perante um simples “quente ao toque”: estávamos perante algo que poderia encurtar a vida do produto ou criar comportamento imprevisível entre ambientes. 

![Original-emperature-test](https://assets2.openterface.com/images/Original-emperature-test.webp)

*Teste de temperatura de referência (interno vs externo)*

---

## Entrada 4: Uma verificação rápida, o fluxo forçado funciona (mas não é uma solução de produto)
Antes de redesenharmos qualquer coisa, queríamos uma validação rápida: se removermos o calor mais depressa, as temperaturas baixam significativamente?

Experimentámos uma configuração de fluxo forçado com um ventilador DIY. Fez o que a física indica: as temperaturas baixaram de forma notável, cerca de 15 °C no nosso teste. Isso confirmou que o problema era um estrangulamento térmico, não artefactos de medição ou comportamento de software.

Também confirmou outra coisa: um ventilador não é compatível com o produto que estamos a construir. O KVM-GO precisa de permanecer compacto, silencioso e autocontido. Assim, o fluxo forçado tornou-se uma ferramenta de diagnóstico, não a resposta final.

![Fan-1png](https://assets2.openterface.com/images/Fan-1png.webp)

*Configuração de arrefecimento ventilador DIY*

![Fan-2](https://assets2.openterface.com/images/Fan-2.webp)

*Arrefecimento ventilador DIY, vista alternativa*

![Temperature-test-fan](https://assets2.openterface.com/images/Temperature-test-fan.webp)

*Teste de temperatura com ventilador*

---

## Entrada 5: Correção passo 1, mover fontes de calor para o exterior (sem quebrar a integridade do sinal)
A primeira correção real foi no PCB. Empurrámos o design o mais possível para colocar os dois chips geradores de calor mais perto do lado exterior.

Isto não foi “apenas mover as peças”. Com DP e VGA, as restrições de roteamento são apertadas. Manter os sinais de alta velocidade limpos, especialmente os pares diferenciais, é não negociável. Colocar ambos os chips para fora tornou o roteamento mais difícil e tivemos de trabalhar com cuidado para não degradar a integridade do sinal.

Comparamos layout e roteamento antigo vs novo e construímos hardware para verificar o comportamento. 

![New-PCB-ayout](https://assets2.openterface.com/images/New-PCB-ayout.webp)

*Layout PCB revisto (chips movidos para fora)*

![Wiring-layout-modification](https://assets2.openterface.com/images/Wiring-layout-modification.webp)

*Roteamento revisto (passo 1)*

![Wiring-layout-modification-2](https://assets2.openterface.com/images/Wiring-layout-modification-2.webp)

*Roteamento revisto (área chave)*

![PCB-ayout-modifications](https://assets2.openterface.com/images/PCB-ayout-modifications.webp)

*PCB revista, construída para validação*

### O que mudou após o passo 1
As térmicas melhoraram, mas detetámos um problema de segunda ordem: a temperatura ainda não se transferia eficazmente para o invólucro. Algumas áreas permaneciam mais quentes do que deviam e a imagem térmica sugeria que o invólucro não actuava como um dissipador adequado.

O passo 1 reduziu a severidade dos pontos quentes internos, mas não resolveu completamente o caminho do calor.  

![Modified-fever-symptoms](https://assets2.openterface.com/images/Modified-fever-symptoms.webp)

*Temperatura após alteração de layout (passo 1)*

![Casing-temperature-test](https://assets2.openterface.com/images/Casing-temperature-test.webp)

*Verificação de transferência de calor do invólucro (após passo 1)*

---

## Entrada 6: Correção passo 2, construir um caminho de calor real (blocos de alumínio CNC mais interface térmica)
Neste ponto tratámos o invólucro como parte do sistema térmico, não apenas como tampa.

Adicionámos:
- blocos de alumínio CNC na pilha de PCB superior e inferior
- material de interface térmica (graxa ou almofada) para acoplar o calor ao alumínio e depois ao invólucro de alumínio

O objetivo era simples: aumentar a área efetiva de dissipação térmica e criar um caminho estável e de baixa resistência para o calor chegar ao invólucro, onde pode dissipar-se em segurança.

![cnc](https://assets2.openterface.com/images/cnc.webp)

*Bloco térmico CNC (passo 2)*

![cnc2](https://assets2.openterface.com/images/cnc2.webp)

*Pormenor do bloco CNC instalado*

### Resultado final após o passo 2
Após adicionar o caminho de condução:
- a temperatura externa estabilizou em torno de 65 °C
- a temperatura interna desceu para cerca de 55 °C

A imagem térmica mostrou o que queríamos ver: a distribuição do calor tornou-se mais uniforme e o invólucro participou finalmente na dissipação em vez de deixar o calor acumular internamente. 

![Temperature-measurement-after-adding-CNC](https://assets2.openterface.com/images/Temperature-measurement-after-adding-CNC.webp)

*Temperatura após condução CNC (passo 2)*

![CNC-machining](https://assets2.openterface.com/images/CNC-machining.webp)

*Temperatura do invólucro após condução CNC*

---

## Nota final
O principal deste problema não foi simplesmente “DP e VGA aquecem mais”. A conversão multiestágio custa mais potência e essa parte é esperada. A lição real foi que, num dispositivo tão pequeno, *para onde vai o calor* importa tanto quanto *quanto calor é gerado*.

O passo 1 (layout) reduziu a severidade dos pontos quentes internos.  
O passo 2 (caminho de condução mecânica) tornou a solução durável e adequada ao produto.

Sem ventilador, sem manuseamento especial pelo utilizador, apenas um design que se comporta de forma previsível.
