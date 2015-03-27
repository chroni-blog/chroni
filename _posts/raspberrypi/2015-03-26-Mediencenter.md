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

Eine der beliebtesten Anwendungen, die im Netz mir dem Raspberry Pi zu finden sind, ist die des Mediencenters. Der Sinn des Ganzen ist das einfache Verwalten und Abspielen von Medien aller Art. Viele steigen derzeit um Filme über Streaming Portale wie Maxdome, Amazon Prime instant video und Netflix anstatt sich Filme auf DVD oder BluRay zu kaufen. Möchte man zusätzlich seine Musik in Form von MP3s abspielen, kann ein Mediencenter die Lösung sein.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/mediencenter/kodi.jpg" />
	<figcaption>
		Kodi - Ein kostenloses und umfangreiches Media Center für verschiedene Betriebssysteme, mit dem man Filme, Fotos und Musik verwalten und abspielen kann.
	</figcaption>
</figure>

Im Netz gibt es einige vielversprechende kostenlose Systeme. Hinter den meisten steckt jeweils eine große oder kleine Community, die das System weiterentwickelt. Dabei kann es monatlich oder sogar wöchentlich zu Updates und Verbesserungen kommen. Viele der Systeme, die sich um das Thema Mediencenter drehen nutzen das Programm **Kodi (früher XBMC)**. Kodi ist ein Programm zur Verwaltung und Abspielen von Filmen, Serien, Musik und Bildern. Die Anzahl der Addons übersteigt locker die 2000, womit man das Programm leicht individuell erweitern kann.

**OpenElec** ist ein System, welches sehr einfach einzurichten ist. Es baut ein eigenes Linux-Betriebssystem um das Programm Kodi herum auf und schafft eine sehr simple und performante Umgebung. Nachfolgend zeige ich, wie man ein solches System einrichtet.

## Voraussetzungen

Bevor wir hier anfangen so ein Mediencenter einzurichten, brauchen wir erst einmal ein paar Dinge:

* Raspberry Pi (am besten Version 2)
* Micro-USB Netzteil (5V, 2A)
* HDMI-Kabel
* Micro-SD Karte (8GB ist ausreichend) mit Adapter
* (optional) Ethernet-Kabel oder USB-WLAN-Stick
* (optional) Raspberry Pi Gehäuse

Sobald man auf Dienste aus dem Internet ( Youtube, Netflix, etc. ) oder auf externe Laufwerke im LAN zugreifen will (Festplatten am Router oder an einem <a href="http://de.wikipedia.org/wiki/Network_Attached_Storage">NAS[^nas]</a>) braucht man natürlich eine Internetverbindung. Falls das jedoch per Ethernet-Kabel sich schwierig gestaltet, nimmt man am besten einen USB-WLAN-Stick. Simpel, klein und günstig auf z.B. Amazon zu kaufen.

[^nas]: NAS: Network Attached Storage, bezeichnet einfach zu verwaltende Dateiserver. Allgemein wird NAS eingesetzt, um ohne hohen Aufwand unabhängige Speicherkapazität in einem Rechnernetz bereitzustellen.

Zusätzlich braucht man einen PC, an dem man die Micro-SD Karte benutzen kann.

## Installieren von OpenElec

Hat man alle Komponenten zusammen, läd man sich am besten zuerst die neueste Version von OpenElec herunter. Unter <a href="http://openelec.tv/get-openelec">OpenElec.tv</a> wählt man das Image für den eigenen Raspberry Pi herunter. Die Datei entpackt man am besten mit <a href="http://www.7-zip.de/">7Zip</a> oder einem ähnlichen Programm.

Sobald man dann die *.img Datei hat, läd man sich als Windows-Benutzer das Programm <a href="http://sourceforge.net/projects/win32diskimager/">Win32 Disk Imager</a> herunter. Mit diesem Programm kann man das OpenElec Betriebssystem direkt auf die SD-Karte schreiben.

**Wichtig**: Den richtigen Laufwerksbuchstaben wählen! Vorher am besten prüfen welchen Buchstaben die SD-Karte belegt hat.
{: .notice-info}

<figure class="forth" style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/mediencenter/
Disk-Image-Warning.png" />
	<img src="{{ site.url }}/images/raspberrypi/mediencenter/
Disk-Image-Complete.png" />
	<figcaption>
		Mit dem Tool Win32 Disk Imager lässt sich leicht das System OpenElec auf eine Micro-SD Karte schreiben.
		Image auswählen, Laufwerk der SD-Karte wählen und auf "Write" klicken. 
	</figcaption>
</figure>

Sobald das erledigt wurde, kann der Raspberry Pi gestartet werden. Zuerst die SD-Karte einstecken, danach HDMI und Strom anschließen. Falls der Fernseher CEC unterstützt kann alles in Kodi mit der eigenen Fernbedienung des TVs gesteuert werden. Wirklich tolles Feature! Ansonsten eine Wireless Maus oder Tastatur anschließen. Später ist es auch möglich eine App fürs Smartphone zur Steuerung zu nutzen.

Zu Beginn wird man Schritt für Schritt durch eine Startkonfiguration geleitet, in der man Sprache, Netzwerk und sonstige Einstellungen vornehmen kann.
Danach kann man unter Videos die Orte seiner Film und Serien Dateien festlegen.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/mediencenter/big_buck_bunny_small.png" />
	<figcaption>
		Big Buck Bunny - Blender Foundation | www.blender.org
	</figcaption>
</figure>

Als Testvideo kann ich <a href="https://peach.blender.org/download/">Big Buck Bunny</a> der <a href="www.blender.org">Blender Foundation</a> empfehlen. Das Video kann kostenfrei in FullHD Qualität (1080p) mit Surround Sound (AC3 und AAC) heruntergeladen werden. Der Raspberry Pi 2 kommt damit ohne Probleme klar.