---
layout: article
title: "Mediencenter mit dem Raspberry Pi"
date: 2015-03-26
modified: 2015-03-26
author: Christian
categories: unpublished
share: true
excerpt: "Der Mini-Computer für Filme, Musik, Serien und mehr."
tags: [raspberrypi, movies, music]
toc: true
comments: true
image:
  feature: 
  teaser: raspberrypi/mediencenter/mediencenter_teaser.png
---

Seit einiger Zeit sind immer über Neuigkeiten und Hobbyprojekte über ihn zu lesen. Der <a href="http://www.raspberrypi.org">Raspberry Pi</a>. Er ist ein kleiner - sehr kleiner - Computer, der unglaublich wenig Strom braucht und sich leicht an jeden Monitor oder Fernseher mit HDMI anschließen lässt. Dabei hat er alles was man für das eigene Hobbyprojekt im Bereich Informatik braucht. Gerade der Preis des Rechners in Scheckkartengröße ist interessant. 

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/raspberry_pi.jpg">
	<figcaption>
		Der Raspberry Pi 2.
	</figcaption>
</figure>

Hier eine Auflistung der wichtigsten Details des Raspberry Pi 2:

* 900MHz Quad-Core ARM Cortex-A7 CPU
* 1GB RAM
* 4 USB Ports
* HDMI Port und Composite Video
* Ethernet Port (LAN)
* 3,5mm Audio
* Micro SD Slot
* **Preis: 35€**

Nicht jeder hat aber das Know-How, die Zeit und die Lust sich mit den Grundfunktionen eines Linux-Betriebssystems herumzuschlagen. **Was kann man also ohne viel Informatik-Kenntnisse mit dem Ding anstellen?**

## Mediencenter

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/mediencenter/kodi.jpg" />
	<figcaption>
		Kodi - Ein kostenloses und umfangreiches Media Center für verschiedene Betriebssysteme, mit dem man Filme, Fotos und Musik verwalten und abspielen kann.
	</figcaption>
</figure>

Eine der beliebtesten Anwendungen, die im Netz mir dem Raspberry Pi zu finden sind, ist die des Mediencenters. Der Sinn des Ganzen ist das einfache Verwalten und Abspielen von Medien aller Art. Viele steigen derzeit um Filme über Streaming Portale wie Maxdome, Amazon Prime instant video und Netflix anstatt sich Filme auf DVD oder BluRay zu kaufen. Möchte man zusätzlich seine Musik in Form von MP3s abspielen, kann ein Mediencenter die Lösung sein.

Im Netz gibt es einige vielversprechende kostenlose Systeme. Hinter den meisten steckt jeweils eine große oder kleine Community, die das System weiterentwickelt. Dabei kann es monatlich oder sogar wöchentlich zu Updates und Verbesserungen kommen. Viele der Systeme, die sich um das Thema Mediencenter drehen nutzen das Programm **Kodi (früher XBMC)**. Kodi ist ein Programm zur Verwaltung und Abspielen von Filmen, Serien, Musik und Bildern. Die Anzahl der Addons übersteigt locker die 2000, womit man das Programm leicht individuell erweitern kann.

**OpenElec** ist ein System, welches sehr einfach einzurichten ist. Es baut ein eigenes Linux-Betriebssystem um das Programm Kodi herum auf und schafft eine sehr simple und performante Umgebung. Nachfolgend zeige ich, wie man ein solches System einrichtet.

## Einrichten von OpenElec

