---
layout: article
title: "Homeautomation mit dem Raspberry Pi - Teil 4"
date: 2016-03-18
modified: 2016-03-18
author: Christian
categories: unpublished
share: true
excerpt: "Temperaturmessung zum Selbstbauen mit dem Raspberry Pi - Einrichten des RPis"
tags: [raspberrypi, homeautomation]
toc: true
comments: true
image:
  feature: 
  teaser: raspberrypi/homeautomation/homeautomation_teaser.png
---

In [Teil 1](../HomeAutomation){:target="_blank"} hab ich einen groben Plan und die Übersicht beschrieben, wobei [Teil 2](../HomeAutomation_2){:target="_blank"} den Aufbau der kleinen Sendermodule beschreibt. 
Der dritte [Teil](../HomeAutomation_3){:target="_blank"} hat gezeigt wie man Code auf das Modul schreibt. Jetzt wird das Empfangsmodul und der Raspberry Pi in Betrieb genommen. Ich nutze hier übrigens einen Raspberry Pi 1. Neuere Versionen sollten aber genauso funktionieren und die selben Schritte enthalten.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/homeautomation/install_raspbian_and_communicate.png">
</figure>

## Raspbian installieren

Im [Mediencenter-Artikel](../Mediencenter){:target="_blank"} wurde das System direkt über ein Image installiert. Jetzt will ich mal eine Alternative über <a href="https://www.raspberrypi.org/downloads/noobs/">NOOBS</a> zeigen. Hier läd man sich entweder NOOBS oder NOOBS Lite herunter. Ich hab hier die Lite Version genommen. Diese entpackt man einfach direkt auf die formatierte und leere SD-Karte. Ab damit in den Raspberry Pi und man kann diesen schon booten lassen!

Bei der NOOBS Lite Variante muss das Betriebssystem zuerst noch heruntergeladen werden. Daher braucht man hier auch einen Netzwerkzugang über Ethernet-Kabel. Anfangs braucht man auch noch einen Bildschirm (TV oder Monitor) und eine Tastatur oder eine Maus. Sobald der Pi hochgefahren ist, kann man sein Betriebssystem wählen. Hier wählen wir "Raspbian" aus (Leertaste zum bestätigen) und installieren es (Shortcut: "i"). Ab jetzt kann man sich eine Weile zurücklehnen und dem Installationsbalken zuschauen wie er sich langsam füllt.
<!-- Noobs Lite herunterladen, auf formatierte SD Karte kopieren.
- SD Karte in RPi stecken
- booten
- Netzwerkkabel (bei Lite) benötigt!
- Raspbian auswählen (Leertaste), installieren (i), warten -->

