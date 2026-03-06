---
draft: false
date: 2026-03-05
title: "Correction thermique DP/VGA KVM-GO – Journal technique"
description: "Analyse approfondie du problème de chaleur DP et VGA sur KVM-GO : mesures, modifications PCB et corrections mécaniques ayant résolu la surchauffe sans ajouter de ventilateur."
keywords: "correction thermique KVM-GO, chaleur DP, chaleur VGA, KVM-over-USB ingénierie, disposition PCB, gestion thermique, Openterface, journal technique"
author: "TechxArtisan Studio"
category: "Mises à jour produit"
tags: ["KVM-GO", "Thermique", "Journal technique", "Conception produit"]
featured: false
social:
  image: "https://assets.openterface.com/images/kvm-go/thermal-fix.webp"
  title: "Résolution de la chaleur DP/VGA sur KVM-GO"
  description: "Comment nous avons corrigé la surchauffe des variantes DP et VGA de KVM-GO via des améliorations de disposition et de conduction."
---

# Journal technique : traquer la chaleur DP/VGA sur KVM-GO (et la solution qui a finalement fonctionné)

## Entrée 1 : Le moment où nous avons réalisé que ce n’était pas une « chaleur normale »
À mi-chemin du développement de KVM-GO, nous avons observé un comportement thermique ne correspondant pas aux attentes habituelles de « petit appareil qui chauffe ». Le problème n’apparaissait que sur deux variantes : DisplayPort (DP) et VGA. La variante HDMI restait dans les limites prévues.

Au début, le symptôme était simple : la température du boîtier devenait inconfortable plus tôt que prévu. Ce qui nous inquiétait n’était pas le confort, mais la possibilité que les températures internes dépassent largement ce que les composants grand public sont censés supporter à long terme.


---

## Entrée 2 : Pourquoi uniquement DP et VGA
En retraçant la conception du chemin vidéo à travers les versions, un schéma est apparu.

- HDMI : une seule étape de conversion (HDMI vers vidéo USB) avec MS2130S
- DP : une chaîne à deux puces (IT6563 + MS2130S) pour convertir DP vers vidéo USB
- VGA : une chaîne à deux puces (MS9288C + MS2109S) pour convertir VGA vers vidéo USB

Deux puces ne font pas qu’ajouter des composants. Elles ajoutent de la dissipation de puissance et des points chauds localisés. Dans un produit de la taille de KVM-GO, ces points chauds ont très peu d’espace pour se diffuser.

Ensuite, nous avons buté sur la deuxième contrainte : la surface. KVM-GO pousse la taille aux limites, ce qui signifie que la surface de PCB et la surface effective de diffusion thermique sont toutes deux minuscules.

Enfin, une contrainte de disposition est devenue un vrai compromis d’ingénierie. Placer les deux puces chaudes du même côté semble idéal thermiquement, mais le brochage et les exigences de routage haute vitesse rendaient cette approche difficile. Mettre une puce plus « à l’intérieur » simplifiait le routage et aidait l’intégrité du signal, mais piégeait la chaleur dans l’intérieur du boîtier.

![Original-PCB-layout](https://assets2.openterface.com/images/Original-PCB-layout.webp)

*Disposition PCB d’origine*

![original-Wiring](https://assets2.openterface.com/images/original-Wiring.webp)

*Routage haute vitesse d’origine*

![KVM-Go-tructure](https://assets2.openterface.com/images/KVM-Go-tructure.webp)


*Empilement interne KVM-GO*

---

## Entrée 3 : Mesurer ce qui compte, température interne vs externe
Nous avons décidé d’arrêter les suppositions et de mesurer les deux côtés du problème. Nous avons mis en place des points de mesure pour la surveillance externe et interne, puis effectué un test de charge prolongé.

Le résultat était alarmant, surtout sur VGA.

Après environ une heure de fonctionnement soutenu :
- la surface externe atteignait environ 65 °C
- la température interne culminait autour de 115 °C

De nombreux composants grand public sont dimensionnés pour des températures maximales d’utilisation autour de 85 °C selon la pièce et le grade. Des températures internes à trois chiffres signifiaient que nous n’étions pas face à un simple « chaud au toucher » : nous avions quelque chose pouvant raccourcir la durée de vie du produit ou créer un comportement imprévisible selon les environnements. 

![Original-emperature-test](https://assets2.openterface.com/images/Original-emperature-test.webp)

*Test de température de référence (interne vs externe)*

---

## Entrée 4 : Un test de cohérence rapide, la ventilation forcée fonctionne (mais ce n’est pas une solution produit)
Avant toute refonte, nous voulions une validation rapide : si on évacue la chaleur plus vite, les températures baissent-elles significativement ?

Nous avons essayé une configuration de ventilation forcée simple avec un ventilateur DIY. Les résultats ont suivi la physique : les températures ont nettement baissé, environ 15 °C dans notre test. Cela a confirmé que le problème était un goulot d’étranglement thermique, et non des artefacts de mesure ou du logiciel.

Cela a aussi confirmé autre chose : un ventilateur n’est pas compatible avec le produit que nous construisons. KVM-GO doit rester compact, silencieux et autonome. La ventilation forcée est donc devenue un outil de diagnostic, pas la réponse finale.

![Fan-1png](https://assets2.openterface.com/images/Fan-1png.webp)

*Configuration de refroidissement ventilateur DIY*

![Fan-2](https://assets2.openterface.com/images/Fan-2.webp)

*Refroidissement ventilateur DIY, vue alternative*

![Temperature-test-fan](https://assets2.openterface.com/images/Temperature-test-fan.webp)

*Test de température avec ventilation*

---

## Entrée 5 : Correctif étape 1, rapprocher les sources de chaleur de l’extérieur (sans dégrader l’intégrité du signal)
La première vraie correction a porté sur la PCB. Nous avons poussé la conception au maximum pour placer les deux puces générant de la chaleur plus près du côté extérieur.

Ce n’était pas « juste déplacer les pièces ». Avec DP et VGA, les contraintes de routage sont serrées. Garder les signaux haute vitesse propres, en particulier les paires différentielles, n’est pas négociable. Mettre les deux puces vers l’extérieur a compliqué le routage, et nous avons dû travailler soigneusement pour éviter de dégrader l’intégrité du signal.

Nous avons comparé l’ancienne et la nouvelle disposition et routage, puis fabriqué du matériel pour valider le comportement. 

![New-PCB-ayout](https://assets2.openterface.com/images/New-PCB-ayout.webp)

*Disposition PCB révisée (puces déplacées vers l’extérieur)*

![Wiring-layout-modification](https://assets2.openterface.com/images/Wiring-layout-modification.webp)

*Routage révisé (pass 1)*

![Wiring-layout-modification-2](https://assets2.openterface.com/images/Wiring-layout-modification-2.webp)

*Routage révisé (zone clé)*

![PCB-ayout-modifications](https://assets2.openterface.com/images/PCB-ayout-modifications.webp)

*PCB révisée, fabriquée pour validation*

### Évolutions après l’étape 1
Les thermiques se sont améliorés, mais nous avons repéré un problème secondaire : la température ne se transférait toujours pas efficacement vers le boîtier. Certaines zones restaient plus chaudes qu’elles ne devraient, et l’imagerie thermique suggérait que le boîtier ne jouait pas le rôle de dissipateur efficace.

L’étape 1 a réduit le pic de stress thermique, mais n’a pas pleinement résolu le chemin de chaleur.  

![Modified-fever-symptoms](https://assets2.openterface.com/images/Modified-fever-symptoms.webp)

*Température après modification de disposition (étape 1)*

![Casing-temperature-test](https://assets2.openterface.com/images/Casing-temperature-test.webp)

*Contrôle du transfert thermique du boîtier (après étape 1)*

---

## Entrée 6 : Correctif étape 2, construire un vrai chemin de chaleur (blocs aluminium CNC + interface thermique)
À ce stade, nous avons traité le boîtier comme une partie du système thermique, et non plus comme un simple couvercle.

Nous avons ajouté :
- des blocs aluminium CNC sur l’empilement PCB supérieur et inférieur
- un matériau d’interface thermique (pâte ou pad) pour coupler la chaleur vers l’aluminium puis vers le boîtier en aluminium

L’objectif était simple : augmenter la surface effective de diffusion thermique et créer un chemin stable et à faible résistance pour que la chaleur atteigne le boîtier, où elle peut se dissiper en toute sécurité.

![cnc](https://assets2.openterface.com/images/cnc.webp)

*Bloc thermique CNC (étape 2)*

![cnc2](https://assets2.openterface.com/images/cnc2.webp)

*Détail du bloc CNC installé*

### Résultat final après l’étape 2
Après ajout du chemin de conduction :
- la température externe s’est stabilisée autour de 65 °C
- la température interne est tombée autour de 55 °C

L’imagerie thermique a montré ce que nous voulions voir : la distribution de chaleur est devenue plus uniforme, et le boîtier a finalement participé à la dissipation au lieu de laisser la chaleur s’accumuler à l’intérieur. 

![Temperature-measurement-after-adding-CNC](https://assets2.openterface.com/images/Temperature-measurement-after-adding-CNC.webp)

*Température après conduction CNC (étape 2)*

![CNC-machining](https://assets2.openterface.com/images/CNC-machining.webp)

*Température du boîtier après conduction CNC*

---

## Conclusion
Leçon de cette affaire : ce n’est pas simplement « DP et VGA chauffent plus ». La conversion multichaîne coûte plus en puissance, et c’est attendu. La vraie leçon est que, dans un appareil aussi petit, *où va la chaleur* compte autant que *combien de chaleur est produite*.

L’étape 1 (disposition) a réduit la sévérité des points chauds internes.  
L’étape 2 (chemin de conduction mécanique) a rendu la solution durable et adaptée au produit.

Pas de ventilateur, pas de manipulation particulière par l’utilisateur, juste une conception qui se comporte de façon prévisible.
