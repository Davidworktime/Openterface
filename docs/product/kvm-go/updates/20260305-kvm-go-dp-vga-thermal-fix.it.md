---
draft: false
date: 2026-03-05
title: "Correzione termica DP/VGA KVM-GO – Registro tecnico"
description: "Analisi approfondita del problema di calore DP e VGA su KVM-GO: misurazioni, modifiche PCB e correzioni meccaniche che hanno risolto il surriscaldamento senza aggiungere ventilatori."
keywords: "correzione termica KVM-GO, calore DP, calore VGA, KVM-over-USB ingegneria, layout PCB, gestione termica, Openterface, registro tecnico"
author: "TechxArtisan Studio"
category: "Aggiornamenti prodotto"
tags: ["KVM-GO", "Termico", "Registro tecnico", "Progettazione prodotto"]
featured: false
social:
  image: "https://assets.openterface.com/images/kvm-go/thermal-fix.webp"
  title: "Risoluzione del calore DP/VGA su KVM-GO"
  description: "Come abbiamo corretto il surriscaldamento delle varianti DP e VGA di KVM-GO tramite miglioramenti al layout e alla conduzione."
---

# Registro tecnico: Indagine sul calore DP/VGA su KVM-GO (e la correzione che ha funzionato)

## Voce 1: Il momento in cui abbiamo capito che non era un "calore normale"
A metà dello sviluppo di KVM-GO, abbiamo osservato un comportamento termico che non corrispondeva alle tipiche aspettative di "piccolo dispositivo che si scalda". Il problema si manifestava solo su due varianti: DisplayPort (DP) e VGA. La variante HDMI rimaneva nei limiti previsti.

Inizialmente il sintomo era semplice: la temperatura del contenitore diventava scomoda prima del previsto. A preoccuparci non era il comfort, ma la possibilità che le temperature interne superassero di gran lunga quanto i componenti consumer sono progettati per tollerare nel tempo.


---

## Voce 2: Perché solo DP e VGA
Analizzando il design del percorso video tra le versioni, è emerso un modello.

- HDMI: un singolo stadio di conversione (HDMI a video USB) con MS2130S
- DP: catena a due chip (IT6563 più MS2130S) per convertire DP in video USB
- VGA: catena a due chip (MS9288C più MS2109S) per convertire VGA in video USB

Due chip non aggiungono solo componenti. Aggiungono dissipazione di potenza e hotspot localizzati. In un prodotto delle dimensioni di KVM-GO, quegli hotspot hanno pochissimo spazio per diffondersi.

Poi abbiamo incontrato il secondo vincolo, la superficie. KVM-GO spinge la dimensione al limite, quindi area PCB e area effettiva di dissipazione termica sono entrambe ridotte.

Infine, un vincolo di layout è diventato un vero compromesso ingegneristico. Mettere entrambi i chip caldi sullo stesso lato sembra ideale termicamente, ma i requisiti di pinout e routing ad alta velocità rendevano difficile questo approccio. Mettere un chip più "all'interno" semplificava il routing e aiutava l'integrità del segnale, ma intrappolava il calore nell'interno del contenitore.

![Original-PCB-layout](https://assets2.openterface.com/images/Original-PCB-layout.webp)

*Layout PCB originale*

![original-Wiring](https://assets2.openterface.com/images/original-Wiring.webp)

*Routing ad alta velocità originale*

![KVM-Go-tructure](https://assets2.openterface.com/images/KVM-Go-tructure.webp)


*Struttura interna dello stack KVM-GO*

---

## Voce 3: Misurare ciò che conta, temperatura interna vs esterna
Abbiamo deciso di smettere di indovinare e misurare entrambi i lati del problema. Abbiamo creato punti di misura della temperatura per monitoraggio esterno e interno, poi eseguito un test di carico prolungato.

Il risultato era allarmante, soprattutto su VGA.

Dopo circa un'ora di funzionamento sostenuto:
- la superficie esterna raggiungeva circa 65 °C
- la temperatura interna piccava intorno ai 115 °C

Molti componenti consumer sono valutati per temperature operative massime intorno agli 85 °C, a seconda del componente e del grado. Vedere temperature interne a tre cifre significava che non stavamo affrontando solo un "caldo al tocco": stavamo guardando qualcosa che poteva accorciare la vita del prodotto o creare comportamenti imprevedibili tra gli ambienti. 

![Original-emperature-test](https://assets2.openterface.com/images/Original-emperature-test.webp)

*Test di temperatura di riferimento (interno vs esterno)*

---

## Voce 4: Un rapido sanity check, il flusso forzato funziona (ma non è una soluzione prodotto)
Prima di ridefinire qualsiasi cosa, volevamo una convalida rapida: se rimuoviamo il calore più velocemente, le temperature scendono in modo significativo?

Abbiamo provato una configurazione di flusso forzato con un ventilatore DIY. Ha fatto quello che la fisica prevede: le temperature sono scese notevolmente, circa 15 °C nel nostro test. Questo ha confermato che il problema era un collo di bottiglia termico, non artefatti di misurazione o comportamento software.

Ha confermato anche altro: un ventilatore non è compatibile con il prodotto che stiamo costruendo. KVM-GO deve restare compatto, silenzioso e autonomo. Quindi il flusso forzato è diventato uno strumento diagnostico, non la risposta finale.

![Fan-1png](https://assets2.openterface.com/images/Fan-1png.webp)

*Setup di raffreddamento ventilatore DIY*

![Fan-2](https://assets2.openterface.com/images/Fan-2.webp)

*Raffreddamento ventilatore DIY, vista alternativa*

![Temperature-test-fan](https://assets2.openterface.com/images/Temperature-test-fan.webp)

*Test temperatura con ventilatore*

---

## Voce 5: Correzione passaggio 1, spostare le sorgenti di calore verso l'esterno (senza compromettere l'integrità del segnale)
La prima vera correzione è stata sul PCB. Abbiamo spinto il design il più possibile verso il posizionamento di entrambi i chip che generano calore più vicino al lato esterno.

Non era "basta spostare i componenti". Con DP e VGA, i vincoli di routing sono stretti. Mantenere i segnali ad alta velocità puliti, soprattutto le coppie differenziali, è non negoziabile. Mettere entrambi i chip verso l'esterno ha reso il routing più difficile, e abbiamo dovuto lavorare con attenzione per non degradare l'integrità del segnale.

Abbiamo confrontato layout e routing vecchi vs nuovi, poi costruito hardware per verificare il comportamento. 

![New-PCB-ayout](https://assets2.openterface.com/images/New-PCB-ayout.webp)

*Layout PCB rivisto (chip spostati verso l'esterno)*

![Wiring-layout-modification](https://assets2.openterface.com/images/Wiring-layout-modification.webp)

*Routing rivisto (passo 1)*

![Wiring-layout-modification-2](https://assets2.openterface.com/images/Wiring-layout-modification-2.webp)

*Routing rivisto (area chiave)*

![PCB-ayout-modifications](https://assets2.openterface.com/images/PCB-ayout-modifications.webp)

*PCB rivista, costruita per validazione*

### Cosa è cambiato dopo il passaggio 1
Le termiche sono migliorate, ma abbiamo individuato un problema di secondo ordine: la temperatura ancora non si trasferiva efficacemente nel contenitore. Alcune aree restavano più calde del dovuto e l'imaging termico suggeriva che il contenitore non agiva come un vero dissipatore di calore.

Il passaggio 1 ha ridotto la severità degli hotspot interni, ma non ha completamente risolto il percorso del calore.  

![Modified-fever-symptoms](https://assets2.openterface.com/images/Modified-fever-symptoms.webp)

*Temperatura dopo modifica layout (passaggio 1)*

![Casing-temperature-test](https://assets2.openterface.com/images/Casing-temperature-test.webp)

*Verifica trasferimento termico del guscio (dopo passaggio 1)*

---

## Voce 6: Correzione passaggio 2, costruire un vero percorso termico (blocchi alluminio CNC più interfaccia termica)
A questo punto abbiamo trattato il contenitore come parte del sistema termico, non solo come copertura.

Abbiamo aggiunto:
- blocchi alluminio CNC sullo stack PCB superiore e inferiore
- materiale per interfaccia termica (pasta o pad) per accoppiare il calore all'alluminio e poi al contenitore in alluminio

L'obiettivo era semplice: aumentare l'area effettiva di dissipazione e creare un percorso stabile a bassa resistenza perché il calore raggiunga il contenitore, dove può dissiparsi in sicurezza.

![cnc](https://assets2.openterface.com/images/cnc.webp)

*Blocco termico CNC (passaggio 2)*

![cnc2](https://assets2.openterface.com/images/cnc2.webp)

*Dettaglio blocco CNC installato*

### Risultato finale dopo il passaggio 2
Dopo l'aggiunta del percorso di conduzione:
- la temperatura esterna si è stabilizzata intorno ai 65 °C
- la temperatura interna è scesa intorno ai 55 °C

L'imaging termico ha mostrato ciò che volevamo: la distribuzione del calore è diventata più uniforme e il contenitore ha finalmente partecipato alla dissipazione invece di lasciare accumulare il calore internamente. 

![Temperature-measurement-after-adding-CNC](https://assets2.openterface.com/images/Temperature-measurement-after-adding-CNC.webp)

*Temperatura dopo conduzione CNC (passaggio 2)*

![CNC-machining](https://assets2.openterface.com/images/CNC-machining.webp)

*Temperatura del guscio dopo conduzione CNC*

---

## Nota finale
La lezione di questo problema non era semplicemente "DP e VGA scaldano di più". La conversione multistadio costa più potenza e quella parte è attesa. La vera lezione era che, in un dispositivo così piccolo, *dove va il calore* conta tanto quanto *quanto calore viene generato*.

Il passaggio 1 (layout) ha ridotto la severità degli hotspot interni.  
Il passaggio 2 (percorso di conduzione meccanica) ha reso la soluzione duratura e adatta al prodotto.

Nessun ventilatore, nessuna gestione speciale da parte dell'utente, solo un design che si comporta in modo prevedibile.
