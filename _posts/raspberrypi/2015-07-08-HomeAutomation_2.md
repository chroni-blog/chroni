---
layout: article
title: "Homeautomation mit dem Raspberry Pi - Teil 2"
date: 2015-07-07
modified: 2015-07-07
author: Christian
categories: unpublished
share: true
excerpt: "Temperaturmessung zum Selbstbauen mit dem Raspberry Pi - Bauen der Funkmodule"
tags: [raspberrypi, homeautomation]
toc: true
comments: true
image:
  feature: 
  teaser: raspberrypi/homeautomation/homeautomation_teaser.png
---

Im ersten Teil dieser Serie, hab ich dene groben [Plan und die Übersicht](../HomeAutomation){:target="_blank"} beschrieben. Hier erklär ich, wie ich die Sendermodule der Hausautomation gebaut hab und zeige was sich damit alles anstellen lässt.
Nun geh ich auf den Bau eines Moduls ein. 

Das wichtigste an dem Modul ist, dass man mehrere unterschiedliche Sensoren anbinden können soll. Die Sensoren sollen z.B. die Temperatur und die Feuchtigkeit messen.

Eine Zusammenstellung des Moduls kann also so aussehen:

| Bauteil         | Bezeichnung | Kosten |
|:----------------|:------------|:-------|
| Platine         |             |		 |
| Funkmodul       |             |        |
| Steuereinheit   | Tiny        |        |
| Sensormodul     | DHT22       |        |
| Batteriegehäuse |             |        |
| Draht/Antenne   |             |        |
| Widerstände     |             |        |
| Gehäuse         |             |        |
|:----------------|:------------|:-------|
|                 | Gesamt      |        |

Hier kann ich wieder Nathan Chantrell danken, weil er die meisten Module schon getestet und den Code abgestimmt hat. Dadurch hatte ich selbst kaum noch Arbeit mit der Suche nach passenden Modulen.

### Abbildung mit Komponenten

Jedes Modul besteht dabei aus einer Platine, einer Steuereinheit, einem Funksendemodul, Batterien und ein oder mehrere Sensoren. Um Strom zu sparen, sendet man nicht andauernd Daten über Funk zur Basisstation. Das würde bei weitem zu viel Strom kosten und würde uns auch nicht sinnvollere Informationen liefern. Temperatur und Feuchtigkeit ändern sich ja schließlich nicht innerhalb weniger Sekunden. 

Auf die Steuereinheit selbst kann man direkt Programmcode kopieren und dann immer wieder ausführen lassen. Hier kann man also selbst festlegen, wie oft man Daten ausliest und schickt. Die Informationen selbst, die in der Nachricht an die Basisstation (den Raspberry Pi) stehen, können natürlich auch selbst festgelegt werden. Ich selbst lasse jedes Modul alle 2 Minuten die Daten an den Raspberry Pi weiterschicken.

Sensoren ermitteln bei "Anfrage" der Steuereinheit die Messdaten an diese wieder zurück. Auch diese werden nur zeitlich vor einem Datenaustausch angesprochen und verbrauchen ansonsten wenig bis keinen Strom. 

