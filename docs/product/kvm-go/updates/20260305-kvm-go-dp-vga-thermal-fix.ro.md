---
draft: false
date: 2026-03-05
title: "Corecție termică DP/VGA KVM-GO – Jurnal de inginerie"
description: "Analiză aprofundată a problemei de căldură DP și VGA pe KVM-GO: măsurători, modificări PCB și corecții mecanice care au rezolvat supraîncălzirea fără a adăuga ventilator."
keywords: "corecție termică KVM-GO, căldură DP, căldură VGA, KVM-over-USB inginerie, layout PCB, management termic, Openterface, jurnal inginerie"
author: "TechxArtisan Studio"
category: "Actualizări produs"
tags: ["KVM-GO", "Termic", "Jurnal inginerie", "Design produs"]
featured: false
social:
  image: "https://assets.openterface.com/images/kvm-go/thermal-fix.webp"
  title: "Rezolvarea căldurii DP/VGA pe KVM-GO"
  description: "Cum am corectat supraîncălzirea variantelor DP și VGA ale KVM-GO prin îmbunătățiri de layout și conducție."
---

# Jurnal de inginerie: Urmărind căldura DP/VGA pe KVM-GO (și corecția care a funcționat în sfârșit)

## Intrare 1: Momentul când am realizat că nu era „cald normal”
La jumătatea dezvoltării KVM-GO, am observat un comportament termic care nu corespundea așteptărilor tipice de „dispozitiv mic care se încălzește”. Problema apărea doar la două variante: DisplayPort (DP) și VGA. Varianta HDMI rămânea în limitele așteptate.

La început simptomul era simplu: temperatura carcasei devenea incomodă mai devreme decât era de așteptat. Ce ne preocupa nu era confortul, ci posibilitatea ca temperaturile interne să fie cu mult peste ceea ce componentele consum sunt gândite să tolereze pe termen lung.


---

## Intrare 2: De ce doar DP și VGA
După trasarea designului traseului video prin versiuni, a apărut un tipar.

- HDMI: un singur stadiu de conversie (HDMI la video USB) folosind MS2130S
- DP: lanț cu două chipuri (IT6563 plus MS2130S) pentru a converti DP în video USB
- VGA: lanț cu două chipuri (MS9288C plus MS2109S) pentru a converti VGA în video USB

Două chipuri nu adaugă doar componente. Adaugă disipare de putere și puncte fierbinți localizate. Într-un produs de mărimea KVM-GO, acele puncte fierbinți au foarte puțin spațiu să se răspândească.

Apoi am dat de a doua restricție: suprafața. KVM-GO împinge dimensiunea la limită, ceea ce înseamnă că atât aria PCB cât și aria efectivă de disipare termică sunt minuscule.

În final, a existat o restricție de layout care s-a transformat într-un compromis real de inginerie. Plasarea ambelor chipuri fierbinți pe aceeași parte sună ideal termic, dar cerințele de pinout și rutare de mare viteză au făcut această abordare dificilă. Plasarea unui chip mai „în interior” a simplificat rutarea și a ajutat integritatea semnalului, dar a capturat căldura în interiorul carcasei.

![Original-PCB-layout](https://assets2.openterface.com/images/Original-PCB-layout.webp)

*Layout PCB original*

![original-Wiring](https://assets2.openterface.com/images/original-Wiring.webp)

*Rutare mare viteză originală*

![KVM-Go-tructure](https://assets2.openterface.com/images/KVM-Go-tructure.webp)


*Structură internă stivă KVM-GO*

---

## Intrare 3: Măsurarea a ceea ce contează, temperatură internă vs externă
Am decis să oprim ghiciturile și să măsurăm ambele părți ale problemei. Am construit puncte de măsurare a temperaturii pentru monitorizare externă și internă, apoi am rulat un test de sarcină de durată lungă.

Rezultatul a fost alarmant, mai ales pe VGA.

După aproximativ o oră de funcționare susținută:
- suprafața externă atingea circa 65 °C
- temperatura internă atingea valori maxime în jur de 115 °C

Multe componente consum sunt specificate pentru temperaturi maxime de funcționare în jur de 85 °C, în funcție de piesă și grad exact. A vedea temperaturi interne la trei cifre însemna că nu aveam de-a face doar cu „fierbinte la atingere”: aveam de-a face cu ceva care ar putea scurta viața produsului sau crea comportament imprevizibil între medii. 

![Original-emperature-test](https://assets2.openterface.com/images/Original-emperature-test.webp)

*Test de temperatură de referință (intern vs extern)*

---

## Intrare 4: O verificare rapidă, fluxul forțat funcționează (dar nu e o soluție de produs)
Înainte de a redesena orice, voiam o validare rapidă: dacă putem elimina căldura mai repede, temperaturile scad semnificativ?

Am încercat o configurație de flux forțat cu un ventilator DIY. A făcut ce spune fizica: temperaturile au scăzut vizibil, aproximativ 15 °C în testul nostru. Asta a confirmat că problema era un blocaj termic, nu artefacte de măsurare sau comportament software.

A confirmat și altceva: un ventilator nu e compatibil cu produsul pe care îl construim. KVM-GO trebuie să rămână compact, silențios și autonom. Astfel fluxul forțat a devenit instrument de diagnostic, nu răspunsul final.

![Fan-1png](https://assets2.openterface.com/images/Fan-1png.webp)

*Configurare răcire ventilator DIY*

![Fan-2](https://assets2.openterface.com/images/Fan-2.webp)

*Răcire ventilator DIY, vedere alternativă*

![Temperature-test-fan](https://assets2.openterface.com/images/Temperature-test-fan.webp)

*Test de temperatură cu ventilator*

---

## Intrare 5: Corecție pas 1, mutarea surselor de căldură spre exterior (fără a rupe integritatea semnalului)
Prima corecție reală a fost pe PCB. Am împins designul cât am putut pentru a plasa ambele chipuri generatoare de căldură mai aproape de partea exterioară.

Nu era „doar mutarea pieselor”. Cu DP și VGA, restricțiile de rutare sunt strânse. Păstrarea semnalelor de mare viteză curate, în special perechile diferențiale, e neegociabilă. Plasarea ambelor chipuri spre exterior a făcut rutarea mai grea și a trebuit să lucrăm cu grijă pentru a nu degrada integritatea semnalului.

Am comparat layout-ul și rutarea veche vs nouă, apoi am construit hardware pentru a verifica comportamentul. 

![New-PCB-ayout](https://assets2.openterface.com/images/New-PCB-ayout.webp)

*Layout PCB revizuit (chipuri mutate spre exterior)*

![Wiring-layout-modification](https://assets2.openterface.com/images/Wiring-layout-modification.webp)

*Rutare revizuită (pas 1)*

![Wiring-layout-modification-2](https://assets2.openterface.com/images/Wiring-layout-modification-2.webp)

*Rutare revizuită (zonă cheie)*

![PCB-ayout-modifications](https://assets2.openterface.com/images/PCB-ayout-modifications.webp)

*PCB revizuit, construit pentru validare*

### Ce s-a schimbat după pas 1
Termica s-a îmbunătățit, dar am identificat o problemă de ordin secundar: temperatura încă nu se transfera eficient în carcasă. Unele zone rămâneau mai fierbinți decât ar trebui, iar imaginea termică sugera că carcasă nu acționa ca un disipator adecvat.

Pasul 1 a redus severitatea punctelor fierbinți interne, dar nu a rezolvat complet traseul căldurii.  

![Modified-fever-symptoms](https://assets2.openterface.com/images/Modified-fever-symptoms.webp)

*Temperatură după schimbare layout (pas 1)*

![Casing-temperature-test](https://assets2.openterface.com/images/Casing-temperature-test.webp)

*Verificare transfer termic carcasă (după pas 1)*

---

## Intrare 6: Corecție pas 2, construirea unui traseu termic real (blocuri aluminiu CNC plus interfață termică)
În acest punct am tratat carcasă ca parte a sistemului termic, nu doar ca capac.

Am adăugat:
- blocuri aluminiu CNC pe stiva PCB superioară și inferioară
- material de interfață termică (pastă sau pad) pentru a cupla căldura în aluminiu și apoi în carcasă de aluminiu

Obiectivul era simplu: creșterea suprafeței efective de disipare termică și crearea unui traseu stabil, cu rezistență scăzută, pentru ca căldura să ajungă la carcasă, unde poate disipa în siguranță.

![cnc](https://assets2.openterface.com/images/cnc.webp)

*Bloc termic CNC (pas 2)*

![cnc2](https://assets2.openterface.com/images/cnc2.webp)

*Detaliu bloc CNC instalat*

### Rezultat final după pas 2
După adăugarea traseului de conducție:
- temperatura externă s-a stabilizat la circa 65 °C
- temperatura internă a scăzut la circa 55 °C

Imaginea termică a arătat ce voiam să vedem: distribuția căldurii a devenit mai uniformă și carcasă a participat în sfârșit la disipare, în loc să lase căldura să se acumuleze intern. 

![Temperature-measurement-after-adding-CNC](https://assets2.openterface.com/images/Temperature-measurement-after-adding-CNC.webp)

*Temperatură după conducție CNC (pas 2)*

![CNC-machining](https://assets2.openterface.com/images/CNC-machining.webp)

*Temperatură carcasă după conducție CNC*

---

## Notă finală
Concluzia acestei probleme nu a fost pur și simplu „DP și VGA se încălzesc mai mult”. Conversia în etape multiple costă mai multă putere și acea parte e de așteptat. Lecția reală a fost că, într-un dispozitiv atât de mic, *unde merge căldura* contează la fel de mult ca *câtă căldură se generează*.

Pasul 1 (layout) a redus severitatea punctelor fierbinți interne.  
Pasul 2 (traseu de conducție mecanică) a făcut soluția durabilă și adecvată produsului.

Fără ventilator, fără manipulare specială din partea utilizatorului, doar un design care se comportă predictibil.
