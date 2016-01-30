---
layout: article
title: "Homeautomation mit dem Raspberry Pi - Teil 3"
date: 2016-01-30
modified: 2016-01-30
author: Christian
categories: unpublished
share: true
excerpt: "Temperaturmessung zum Selbstbauen mit dem Raspberry Pi - Programmieren der Funkmodule"
tags: [raspberrypi, homeautomation]
toc: true
comments: true
image:
  feature: 
  teaser: raspberrypi/homeautomation/homeautomation_teaser.png
---

Mit Teil 1 hab ich einen groben [Plan und die Übersicht](../HomeAutomation){:target="_blank"} beschrieben, wobei Teil 2 den Aufbau der kleinen Sendermodule beschreibt. In diesem Artikel beschreibe ich wie man nun Code auf die Chips (ATTiny) der Sendermodule bekommt und was man damit alles anstellen kann.

## Bilder!!
<!--
<figure class="third" style="text-align: center">
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/fertiges_modul.jpg">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/fertiges_modul_small.jpg">
	</a>
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/fertiges_modul2.jpg">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/fertiges_modul2_small.jpg">
	</a>
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/fertiges_modul3.jpg">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/fertiges_modul3_small.jpg">
	</a>
	<figcaption>
		Ein Beispiel eines fertigen Moduls. Hängt bei mir direkt oben in der Ecke an einem Fenster.
	</figcaption>
</figure>-->

## USB Programmierer

Um den ATTiny programmieren zu können braucht man ein besonderes Programmiermodul, wie z.B. den <a href="http://www.ebay.de/itm/New-USBASP-USBISP-AVR-Programmer-USB-ATMEGA8-ATMEGA128-/151302570060?hash=item233a56004c:g:RqgAAOxyIPNTcwx~">USBASP AVR Programmer</a>. Daran steckt man am besten einen <a href="http://www.ebay.de/itm/1x-ITC-14A-14PIN-IC-TEST-CLIPS-/181211343253?hash=item2a3109a995:g:9DoAAOxykYtSKZif">ITC-14A Test Clip</a> den man dann direkt an den Chip klemmen kann. Damit hat man den Vorteil zu anderen Programmierern, dass man auch einen fest angelöteten ATTiny unkompliziert im Nachhinein programmieren kann.
Wie man den USB Programmierer mit dem Clip, und damit direkt mit dem ATTiny, verbindet hab ich hier mal dargestellt:

<figure class="half" style="text-align: center">
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/ITC_Clip_small.png">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/ITC_Clip.png">
	</a>
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/ITC_Clip_photo_small.jpg">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/ITC_Clip_photo.jpg">
	</a>
	<figcaption>
		Links: Verbindungsplan des USB Programmierers mit dem ITC Test Clip (ATTiny).
		Rechts: Fertiger Programmierer und ein ATTiny daneben.
	</figcaption>
</figure>

Jetzt fehlt noch der richtige Treiber für den Programmierer. Den findet man <a href="http://www.fischl.de/usbasp/">hier</a> unter "Drivers". Unter Umständen (gerade unter Windows 8.1) muss man die <a href="http://www.pc-magazin.de/ratgeber/windows-8-1-treibersignierung-ausschalten-abschalten-deaktivieren-windows-8-tipp-1939952.html">Treibersignierung ausschalten</a>. Leider hat wohl Microsoft die Treiber für den USBasp nicht signiert. Aber keine Panik! Nachdem man die Treiber installiert hat kann man die Treibersignierung auch wieder aktivieren.

## Arduino Setup

Hat man den Programmierer fertig gehts nun endlich in Richtung Software. Der Code für den ATtiny selbst wird in C geschrieben. Für die, die nicht programmieren können: Kein Problem! Es gibt mehrere Beispielprogramme wo man nur sehr wenig anpassen muss. Der Code kann ganz bequem vom Windows-Rechner über USB an den ATTiny, die Recheneinheit des Moduls, übertragen werden. Die nötige Software dazu heißt <a href="https://www.arduino.cc/">Arduino</a>. Das Programm ist ein Open Source Projekt welches auf allen gängigen Betriebssystemen (Windows, Linux, Mac OS) läuft. Ich selbst nutze die Version 1.6.0.

Nach kurzer Installation muss man noch die passenden Libraries für den ATtiny installieren. Diese werden in Arduino auch boards genannt. Hierzu läd man sich einfach die aktuellsten <a href="https://code.google.com/archive/p/arduino-tiny/downloads">arduino-tiny boards</a> als ZIP-Archiv runter. Arduino hat unter Windows während der Installation einen Ordner in "Dokumente" erstellt (z.B. C:\Users\<Benutzername>\Documents\Arduino). Hier kopiert man nun den Ordner "tiny" aus dem ZIP-Archiv in den Ordner hardware sodass folgende Ordnerstruktur vorliegt: C:\Users\<Benutzername>\Documents\Arduino\hardware\tiny\avr...

Hat man die Dateien richtig kopiert sollte man nun nach einem Neustart von Arduino unter Tools->Board->ATtiny84 @ 8Mhz (internal oszillator, BOD disabled) anwählen können.

<figure style="text-align: center">
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/arduino_board_selection_small.png">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/arduino_board_selection.png">
	</a>
	<figcaption>
		Auswahl des richtigen Boards in Arduino.
	</figcaption>
</figure>

Ab jetzt kann man den USB Programmierer und die Verkabelung testen. Ist alles richtig angeschlossen kann man unter Tools->Burn Bootloader dem ATtiny eine Frequenz von 8Mhz zuweisen. Ein wirklicher Bootloader wird dabei aber nicht geschrieben, da der ATtiny so einen garnicht nutzt.
Ist alles korrekt verlaufen sollte man folgendes sehen:
<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/homeautomation/burn_bootloader.PNG">
	<figcaption>
		Ausgabefenster nach korrektem Ausführen von Tools->Burn Bootloader.
	</figcaption>
</figure>
Ist irgendetwas schief gelaufen, z.B. der ATtiny nicht korrekt verbunden, erscheint eine Fehlermeldung. Am besten nochmal genau die Verbindungen checken!

## Code schreiben