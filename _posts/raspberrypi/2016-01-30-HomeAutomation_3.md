---
layout: article
title: "Homeautomation mit dem Raspberry Pi - Teil 3"
date: 2016-01-30
modified: 2016-01-30
author: Christian
categories: raspberrypi
share: true
excerpt: "Temperaturmessung zum Selbstbauen mit dem Raspberry Pi - Programmieren der Funkmodule"
tags: [raspberrypi, homeautomation]
toc: true
comments: true
image:
  feature: 
  teaser: raspberrypi/homeautomation/homeautomation_teaser.png
---

In [Teil 1](../HomeAutomation){:target="_blank"} hab ich einen groben Plan und die Übersicht beschrieben, wobei [Teil 2](../HomeAutomation_2){:target="_blank"} den Aufbau der kleinen Sendermodule beschreibt. In diesem Artikel geht es darum wie man nun Code auf die Chips (ATTiny) der Sendermodule bekommt.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/homeautomation/code_to_module.png">
</figure>

## USB Programmierer

Um den ATTiny programmieren zu können, braucht man ein Modul, welches den Code von einem PC auf den Chip überträgt. Z.B. den <a href="http://www.ebay.de/itm/New-USBASP-USBISP-AVR-Programmer-USB-ATMEGA8-ATMEGA128-/151302570060?hash=item233a56004c:g:RqgAAOxyIPNTcwx~">USBASP AVR Programmer</a>. Daran steckt man am besten einen <a href="http://www.ebay.de/itm/1x-ITC-14A-14PIN-IC-TEST-CLIPS-/181211343253?hash=item2a3109a995:g:9DoAAOxykYtSKZif">ITC-14A Test Clip</a>, den man dann direkt an den Chip klemmen kann. Das hat den Vorteil, dass man auch einen fest angelöteten ATTiny unkompliziert im Nachhinein programmieren kann.
Wie man den USB Programmierer mit dem Clip, und damit direkt mit dem ATTiny, verbindet hab ich hier dargestellt:

<figure class="half" style="text-align: center">
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/ITC_Clip.png">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/ITC_Clip_small.png">
	</a>
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/ITC_Clip_photo.jpg">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/ITC_Clip_photo_small.jpg">
	</a>
	<figcaption>
		Links: Verbindungsplan des USB Programmierers mit dem ITC Test Clip (ATTiny).
		Rechts: Fertiger Programmierer und ein ATTiny daneben.
	</figcaption>
</figure>

Jetzt fehlt noch der richtige Treiber für den Programmierer. Den findet man <a href="http://www.fischl.de/usbasp/">hier</a> unter "Drivers". Unter Umständen (besonders unter Windows 8.1) muss man die <a href="http://www.pc-magazin.de/ratgeber/windows-8-1-treibersignierung-ausschalten-abschalten-deaktivieren-windows-8-tipp-1939952.html">Treibersignierung ausschalten</a>. Leider hat wohl Microsoft die Treiber für den USBasp nicht signiert. Aber keine Panik! Nachdem man die Treiber installiert hat kann man die Treibersignierung auch wieder aktivieren.

## Arduino Setup

Hat man den Programmierer fertig gehts nun endlich in Richtung Software. Der Code für den ATTiny selbst wird in C geschrieben. Für die, die nicht programmieren können: Kein Problem! Es gibt mehrere Beispielprogramme wo man nur sehr wenig anpassen muss. Der Code kann ganz bequem vom Windows-Rechner über USB an den ATTiny, die Recheneinheit des Moduls, übertragen werden. Die nötige Software dazu heißt <a href="https://www.arduino.cc/">Arduino</a>. Das Programm ist ein Open Source Projekt, welches auf allen gängigen Betriebssystemen (Windows, Linux, Mac OS) läuft. Ich selbst nutze die Version 1.6.0.

Nach kurzer Installation muss man noch die passenden Bibliotheken für den ATTiny installieren. Diese werden in Arduino auch boards genannt. Hierzu läd man sich einfach die aktuellsten <a href="https://code.google.com/archive/p/arduino-tiny/downloads">arduino-tiny boards</a> als ZIP-Archiv runter. Arduino hat unter Windows während der Installation einen Ordner in "Dokumente" erstellt (z.B. C:\Users\\<Benutzername>\Documents\Arduino). Hier kopiert man nun den Ordner "tiny" aus dem ZIP-Archiv in den Ordner "hardware", sodass folgende Ordnerstruktur vorliegt:

> C:\Users\\<Benutzername>\Documents\Arduino\hardware\tiny\avr...

Hat man die Dateien richtig kopiert sollte man nun nach einem Neustart von Arduino unter Tools->Board->ATtiny84 @ 8Mhz (internal oszillator, BOD disabled) anwählen können.

<figure style="text-align: center">
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/arduino_board_selection.png">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/arduino_board_selection_small.png">
	</a>
	<figcaption>
		Auswahl des richtigen Boards in Arduino.
	</figcaption>
</figure>

Ab jetzt kann man den USB Programmierer und die Verkabelung testen. Ist alles richtig angeschlossen kann man unter Tools->Burn Bootloader dem ATTiny eine Frequenz von 8Mhz zuweisen. Ein wirklicher Bootloader wird dabei aber nicht geschrieben, da der ATTiny so etwas nicht nutzt.
Ist alles korrekt verlaufen sollte man folgendes sehen:
<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/homeautomation/burn_bootloader.PNG">
	<figcaption>
		Ausgabefenster nach korrektem Ausführen von Tools->Burn Bootloader.
	</figcaption>
</figure>
Ist irgendetwas schief gelaufen, z.B. der ATTiny nicht korrekt verbunden, erscheint eine Fehlermeldung. Am besten nochmal genau die Verbindungen checken!

## Code schreiben

Den Code, den man braucht um Temperatur, Feuchtigkeit und Batteriestand eines Moduls auszulesen, bekommt man direkt über <a href="https://github.com/nathanchantrell/TinyTX">Nathans Github-Seite</a>. Der Code ist unter der <a href="http://creativecommons.org/licenses/by-sa/3.0/">Creative Commons Attribution-ShareAlike 3.0 Unported</a> (CC BY-SA 3.0) freigegeben. Das bedeutet unter anderem, dass man den Code verändern, erweitern und sogar für kommerzielle Projekte frei nutzen darf.

Ich werde hier jetzt nicht auf den kompletten Code und seine Einzelheiten eingehen. Um jedoch den Code so anpassen zu können, dass man mehrere DHT22 Funkmodule bauen kann, werde ich die relevanten Stellen kurz beschreiben. Wenn man Erweiterungen, wie z.B. einen Fensterkontaktsensor MC38 nutzen will, nutzt hier die Kommentarfunktion. Ich helf da gern weiter!

{% highlight c style=friendly %}
#include <DHT22.h> // https://github.com/nathanchantrell/Arduino-DHT22
#include <JeeLib.h> // https://github.com/jcw/jeelib
{% endhighlight %}

Der erste Teil des Codes bindet zwei wichtige Bibliotheken ein, die man sich herunterladen und in den Ordner "C:\Users\<Benutzername>\Documents\Arduino\libraries" kopieren muss. Die Bibliothek für den <a href="https://github.com/nathanchantrell/Arduino-DHT22">DHT22</a> ermöglicht einfaches Auslesen und Berechnen der Temperatur und Feuchtigkeitsdaten. <a href="https://github.com/jcw/jeelib">Jeelib</a> ist eine Bibliothek mit Funktionen zur effizienten Energienutzung und Nutzung von Ruhephasen. Das Funkmodul soll nämlich fast die ganze Zeit "schlafen" und nur ab und zu ein Update der Daten senden.

{% highlight c style=friendly %}
#define myNodeID 18      // RF12 node ID in the range 1-30
#define network 210      // RF12 Network group
#define freq RF12_433MHZ // Frequency of RFM12B module
{% endhighlight %}

Danach wird die ID 18, die Netzgruppe 210 und die Frequenz von 433Mhz gesetzt. Die ID könnt ihr zwischen 1-30 frei wählen. Wichtig: <b>Jedes Modul braucht eine eigene ID!</b> Es darf also keine ID doppelt vorkommen. Am besten man schreibt sie sich direkt auf die Rückseite des Moduls und macht eine Liste. Dann behält man auch bei mehreren Modulen den Überblick.

{% highlight c style=friendly %}
int minutes = 5;
for (byte i = 0; i < minutes; ++i){
	Sleepy::loseSomeTime(60000); //JeeLabs power save function: enter low power mode for 60 seconds (valid range 16-65000 ms)
}
{% endhighlight %}

Zum Schluss kann man noch die Sendehäufigkeit einstellen. Als Standard sind 60.000 Millisekunden eingestellt. Das würde bedeuten, dass das Modul jede Minute ein Update senden würde. Ich finde jedoch, dass Temperatur und Feuchtigkeit sich nicht so schnell ändern. Eine For-Schleife um die Funktion "loseSomeTime()" verlängert die Intervalle auf z.B. 5 Minuten. Damit sollte man auch nicht alle 6 Monate die Batterien wechseln müssen.


Mit ein wenig Programmiererfahrung kann man die Logik und die Möglichkeiten natürlich stark erweitern:
Lötet man eine Leuchtdiode an das Modul, kann man auch den Status einer LED (an, aus oder blinkend) prüfen. Damit bekomm ich dann sogar mit, wenn der Waschgang meiner Waschmaschine fertig ist.
Man kann auch zweifarbige (grün/rot) LEDs an das Modul löten um die Funkverbindung über größere Distanzen (2 Stockwerke) zu testen. Grünes Licht für eine gelungene Übertragung, rotes Licht für einen Fehler.
Schreibt ruhig eure Ideen/Umsetzungen hier in die Kommentare rein!

Damit ist das Einrichten der Sendemodule abgeschlossen. Im nächsten Teil beschreib ich die Einrichtung des Raspberry Pis, einer MySQL Datenbank und der Weboberfläche.
Ab dann können wir auch endlich die Funkverbindung testen und zuschauen wie die ersten Daten ankommen!