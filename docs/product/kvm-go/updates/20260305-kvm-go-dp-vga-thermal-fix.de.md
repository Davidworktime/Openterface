---
draft: false
date: 2026-03-05
title: "KVM-GO DP/VGA Wärme-Korrektur – Engineering Log"
description: "Eine detaillierte Betrachtung des DP- und VGA-Hitzeproblems bei KVM-GO: Messungen, PCB-Änderungen und mechanische Korrekturen, die die Überhitzung ohne Lüfter behoben haben."
keywords: "KVM-GO Wärme-Korrektur, DP Hitze, VGA Hitze, KVM-over-USB Engineering, PCB-Layout, Wärmemanagement, Openterface, Engineering Log"
author: "TechxArtisan Studio"
category: "Produkt-Updates"
tags: ["KVM-GO", "Wärme", "Engineering Log", "Produktdesign"]
featured: false
social:
  image: "https://assets.openterface.com/images/kvm-go/thermal-fix.webp"
  title: "KVM-GO DP/VGA Hitze gelöst"
  description: "Wie wir die Überhitzung der DP- und VGA-Varianten von KVM-GO durch Layout- und Leitungsverbesserungen behoben haben."
---

# Engineering Log: DP/VGA-Hitze bei KVM-GO aufspüren (und die Lösung, die endlich funktionierte)

## Eintrag 1: Der Moment, als wir merkten, dass es kein „normales Warm“ war
Mitten in der KVM-GO-Entwicklung beobachteten wir ein Wärmeverhalten, das nicht den üblichen Erwartungen eines „kleinen Geräts, das warm wird“ entsprach. Es trat nur bei zwei Varianten auf: DisplayPort (DP) und VGA. Die HDMI-Variante blieb innerhalb der Erwartungen.

Zunächst war das Symptom einfach: Die Gehäusetemperatur wurde früher als erwartet unangenehm. Was uns beunruhigte, war nicht der Komfort, sondern die Möglichkeit, dass die Innentemperaturen weit über dem liegen, was Verbraucher-Komponenten langfristig tolerieren sollen.


---

## Eintrag 2: Warum nur DP und VGA
Nach der Verfolgung des Videopfs-Designs über die Versionen zeichnete sich ein Muster ab.

- HDMI: eine einzelne Konvertierungsstufe (HDMI zu USB-Video) mit MS2130S
- DP: eine Zwei-Chip-Kette (IT6563 plus MS2130S), um DP in USB-Video zu wandeln
- VGA: eine Zwei-Chip-Kette (MS9288C plus MS2109S), um VGA in USB-Video zu wandeln

Zwei Chips bedeuten nicht nur mehr Teile. Sie bringen mehr Leistungsaufnahme und lokale Hotspots. Bei einem Produkt in KVM-GO-Größe haben diese Hotspots kaum Platz, sich zu verteilen.

Dann stießen wir auf die zweite Einschränkung: die Oberfläche. KVM-GO drückt die Größe ans Limit, was bedeutet, dass PCB-Fläche und effektive Wärmeabgabe-Fläche beide winzig sind.

Schließlich wurde eine Layout-Einschränkung zu einem echten Engineering-Kompromiss. Beide heißen Chips auf dieselbe Seite zu legen klingt thermisch ideal, aber Pinbelegung und High-Speed-Routing-Anforderungen machten diesen Ansatz schwierig. Einen Chip mehr „innen“ zu platzieren vereinfachte das Routing und half der Signalintegrität, fängt aber die Wärme im Inneren des Gehäuses ein.

![Original-PCB-layout](https://assets2.openterface.com/images/Original-PCB-layout.webp)

*Ursprüngliches PCB-Layout*

![original-Wiring](https://assets2.openterface.com/images/original-Wiring.webp)

*Ursprüngliche High-Speed-Verteilung*

![KVM-Go-tructure](https://assets2.openterface.com/images/KVM-Go-tructure.webp)


*KVM-GO internes Stapellayout*

---

## Eintrag 3: Messen, was zählt – Innen- vs. Außentemperatur
Wir beschlossen, mit dem Raten aufzuhören und beide Seiten des Problems zu messen. Wir bauten Temperaturmessstellen für externe und interne Überwachung und führten einen Langzeit-Lasttest durch.

Das Ergebnis war alarmierend, besonders bei VGA.

Nach etwa einer Stunde Dauerbetrieb:
- Außenfläche erreichte etwa 65 °C
- Innentemperatur erreichte Spitzen um 115 °C

Viele Verbraucher-Komponenten sind für maximale Betriebstemperaturen um 85 °C spezifiziert, je nach Teil und Qualitätsstufe. Dreistellige Innentemperaturen bedeuteten, dass wir nicht nur mit „heiß anfassen“ zu tun hatten, sondern mit etwas, das die Produktlebensdauer verkürzen oder unvorhersehbares Verhalten in verschiedenen Umgebungen verursachen könnte. 

![Original-emperature-test](https://assets2.openterface.com/images/Original-emperature-test.webp)

*Basis-Temperaturtest (innen vs. außen)*

---

## Eintrag 4: Ein schneller Sanity-Check – erzwungene Luftströmung funktioniert (aber ist keine Produktlösung)
Bevor wir etwas neu entwarfen, wollten wir eine schnelle Validierung: Wenn wir Wärme schneller abführen, sinken die Temperaturen spürbar?

Wir probierten ein einfaches Setup mit DIY-Lüfter. Es tat, was die Physik sagt: Die Temperaturen sanken deutlich, grob 15 °C in unserem Test. Das bestätigte, dass es ein thermischer Flaschenhals war, kein Messartefakt oder Softwareverhalten.

Es bestätigte auch etwas anderes: Ein Lüfter ist nicht mit dem Produkt vereinbar, das wir bauen. KVM-GO muss kompakt, leise und autark bleiben. Erzwungene Luftströmung wurde also ein Diagnosewerkzeug, nicht die finale Antwort.

![Fan-1png](https://assets2.openterface.com/images/Fan-1png.webp)

*DIY-Lüfter-Kühlungsaufbau*

![Fan-2](https://assets2.openterface.com/images/Fan-2.webp)

*DIY-Lüfterkühlung, alternative Ansicht*

![Temperature-test-fan](https://assets2.openterface.com/images/Temperature-test-fan.webp)

*Temperaturtest mit Lüfterkühlung*

---

## Eintrag 5: Fix Schritt 1 – Wärmequellen nach außen (ohne Signalintegrität zu brechen)
Der erste echte Fix war auf dem PCB. Wir trieben die Konstruktion so weit wie möglich, beide wärmeerzeugenden Chips näher an die Außenseite zu platzieren.

Das war nicht „einfach Teile verschieben“. Bei DP und VGA sind die Routing-Einschränkungen eng. High-Speed-Signale sauber zu halten, besonders die differentiellen Paare, ist nicht verhandelbar. Beide Chips nach außen zu setzen machte das Routing schwieriger, und wir mussten sorgfältig arbeiten, um die Signalintegrität nicht zu verschlechtern.

Wir verglichen altes vs. neues Layout und Routing und bauten Hardware zur Verifikation. 

![New-PCB-ayout](https://assets2.openterface.com/images/New-PCB-ayout.webp)

*Überarbeitetes PCB-Layout (Chips nach außen verlagert)*

![Wiring-layout-modification](https://assets2.openterface.com/images/Wiring-layout-modification.webp)

*Überarbeitete Verteilung (Durchlauf 1)*

![Wiring-layout-modification-2](https://assets2.openterface.com/images/Wiring-layout-modification-2.webp)

*Überarbeitete Verteilung (Schlüsselbereich)*

![PCB-ayout-modifications](https://assets2.openterface.com/images/PCB-ayout-modifications.webp)

*Überarbeitetes PCB, zur Validierung aufgebaut*

### Was sich nach Schritt 1 änderte
Die Wärme verbesserte sich, aber wir entdeckten ein Problem zweiter Ordnung: Die Temperatur übertrug sich immer noch nicht effektiv ins Gehäuse. Einige Bereiche blieben wärmer als sie sollten, und die Thermografie legte nahe, dass das Gehäuse nicht wie ein ordentlicher Wärmeverteiler wirkte.

Schritt 1 reduzierte die Spitzenwärmebelastung, löste aber den Wärmepfad nicht vollständig.  

![Modified-fever-symptoms](https://assets2.openterface.com/images/Modified-fever-symptoms.webp)

*Temperatur nach Layoutänderung (Schritt 1)*

![Casing-temperature-test](https://assets2.openterface.com/images/Casing-temperature-test.webp)

*Gehäuse-Wärmeübertragungsprüfung (nach Schritt 1)*

---

## Eintrag 6: Fix Schritt 2 – einen echten Wärmepfad bauen (CNC-Aluminiumblöcke plus thermische Schnittstelle)
An diesem Punkt behandelten wir das Gehäuse als Teil des thermischen Systems, nicht nur als Abdeckung.

Wir fügten hinzu:
- CNC-Aluminiumblöcke am oberen und unteren PCB-Stapel
- thermisches Schnittstellenmaterial (Wärmeleitpaste oder Pad), um Wärme in das Aluminium und dann in das Aluminiumgehäuse zu koppeln

Das Ziel war einfach: die effektive Wärmeverteilerfläche vergrößern und einen stabilen, niederohmigen Pfad schaffen, damit Wärme zum Gehäuse gelangt, wo sie sicher abgeführt werden kann.

![cnc](https://assets2.openterface.com/images/cnc.webp)

*CNC-Wärmeblock (Schritt 2)*

![cnc2](https://assets2.openterface.com/images/cnc2.webp)

*CNC-Block eingebaut, Detail*

### Endergebnis nach Schritt 2
Nach Hinzufügen des Leitpfads:
- Außentemperatur stabilisierte sich bei etwa 65 °C
- Innentemperatur sank auf etwa 55 °C

Die Thermografie zeigte, was wir sehen wollten: Die Wärmeverteilung wurde gleichmäßiger, und das Gehäuse beteiligte sich endlich an der Ableitung, anstatt Wärme intern anzustauen. 

![Temperature-measurement-after-adding-CNC](https://assets2.openterface.com/images/Temperature-measurement-after-adding-CNC.webp)

*Temperatur nach CNC-Leitung (Schritt 2)*

![CNC-machining](https://assets2.openterface.com/images/CNC-machining.webp)

*Gehäusetemperatur nach CNC-Leitung*

---

## Abschlussbemerkung
Die Erkenntnis aus diesem Problem war nicht einfach „DP und VGA werden wärmer“. Mehrstufige Konvertierung kostet mehr Leistung, und das ist erwartbar. Die eigentliche Lektion war: In einem so kleinen Gerät spielt es eine Rolle, *wohin* die Wärme geht, genauso wie *wie viel* Wärme erzeugt wird.

Schritt 1 (Layout) reduzierte die Schwere der internen Hotspots.  
Schritt 2 (mechanischer Leitpfad) machte die Lösung dauerhaft und produktgeeignet.

Kein Lüfter, keine spezielle Benutzerbehandlung, nur ein Design, das sich vorhersehbar verhält.
