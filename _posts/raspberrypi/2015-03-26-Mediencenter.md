---
layout: article
title: "Mediencenter mit dem Raspberry Pi"
date: 2015-03-26
modified: 2015-03-26
author: Christian
categories: raspberrypi
share: true
excerpt: "Der Mini-Computer für Filme, Musik, Serien und mehr."
tags: [raspberrypi, movies, music]
toc: true
comments: true
image:
  feature: 
  teaser: raspberrypi/mediencenter/mediencenter_teaser.png
---

Seit einiger Zeit sind immer über Neuigkeiten und Hobbyprojekte über ihn zu lesen. Der <a href="http://www.raspberrypi.org">Raspberry Pi</a>. Er ist ein kleiner - sehr kleiner - Computer, der unglaublich wenig Strom braucht und sich leicht an jeden Monitor oder Fernseher per HDMI anschließen lässt. Er hat alles was man für das eigene Hobbyprojekt im Bereich Informatik braucht. Gerade der Preis und Größe des Rechners sind unschlagbar.

Nicht jeder hat aber das Know-How, die Zeit und die Lust sich mit den Grundfunktionen eines Linux-Betriebssystems herumzuschlagen. **Was kann man also ohne viel Informatik-Kenntnisse mit einem Raspberry Pi anstellen?**

## Der Raspberry Pi 2:

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

Mit der Version 2 des kleinen Computers ist es möglich eine Linux-Distribution oder eine kostenlose Version von <a href="http://dev.windows.com/de-de/featured/raspberrypi2support">Windows 10</a> zu nutzen.


## Mediencenter

Eine der beliebtesten Anwendungen, die im Netz mir dem Raspberry Pi zu finden sind, ist die des Mediencenters. Der Sinn des Ganzen ist das einfache **Verwalten und Abspielen von Medien aller Art**. Viele Heimanwender steigen derzeit vo Kauf von BluRay und DVD auf Streaming Portale wie Maxdome, Amazon Prime instant video und Netflix um. Dadurch spart man sich z.B. Platz im Regal und den Weg zum Händler bzw. Versandkosten. Möchte man zusätzlich seine Musik in Form von MP3s abspielen, kann ein Mediencenter die Lösung sein.

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

Man sollte dafür nicht mehr als ca. 60-80€ ausgeben müssen.
Sobald man auf Dienste aus dem Internet ( Youtube, Netflix, etc. ) oder auf externe Laufwerke im LAN zugreifen will (Festplatten am Router oder an einem <a href="http://de.wikipedia.org/wiki/Network_Attached_Storage">NAS[^nas]</a>) braucht man natürlich eine Netzwerkverbindung. Falls das jedoch per Ethernet-Kabel sich schwierig gestaltet, nimmt man am besten einen USB-WLAN-Stick. Simpel, klein und günstig auf z.B. Amazon zu kaufen.

[^nas]: NAS: Network Attached Storage, bezeichnet einfach zu verwaltende Dateiserver. Allgemein wird NAS eingesetzt, um ohne hohen Aufwand unabhängige Speicherkapazität in einem Rechnernetz bereitzustellen.

Zusätzlich braucht man einen PC oder Laptop, an dem man die Micro-SD Karte benutzen kann.

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

Sobald das erledigt wurde, kann der Raspberry Pi gestartet werden. Zuerst die SD-Karte einstecken, danach HDMI und Strom anschließen. Falls der Fernseher CEC unterstützt kann alles in Kodi mit der eigenen Fernbedienung des TVs gesteuert werden. Wirklich tolles Feature! Ansonsten einfach eine Maus oder Tastatur (Empfehlung: Logitech K400) anschließen. Später ist es auch möglich eine Smartphone-App zur Steuerung zu nutzen.

Zu Beginn wird man Schritt für Schritt durch eine Startkonfiguration geleitet, in der man Sprache, Netzwerk und sonstige Einstellungen vornehmen kann. Danach befindet man sich schon im Hauptmenü. Hier 

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/mediencenter/openelec_start.png" />
	<figcaption>
		Erster Start von OpenElec. Hier wird man nach und nach durch die grundlegenden Einstellungen geführt.
	</figcaption>
</figure>

Danach kann man unter Videos die Orte seiner Film und Serien Dateien festlegen. 
Als Testvideo kann ich <a href="https://peach.blender.org/download/">Big Buck Bunny</a> der <a href="www.blender.org">Blender Foundation</a> empfehlen. Das Video kann kostenfrei in FullHD Qualität (1080p) mit Surround Sound (AC3 und AAC) heruntergeladen werden. Sobald das Testvideo auf einem USB-Stick oder einer externen Festplatte direkt an den Raspberry Pi per USB angesteckt ist, kanns losgehen. Im Hauptmenü unter Videos wählt man "Dateien" aus. Hier könnte man jetzt direkt auf den Datenträger zugreifen und das Video abspielen.

<figure class="forth" style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/mediencenter/kodi_usb_buck_small.jpg" />
	<figcaption>
		
	</figcaption>
</figure>

Es könnte aber lästig werden jedes mal die Filme oder Serien direkt auf den Festplatten zu suchen (gerade wenn man dort keine Ordnung hat). Deswegen gibt es unter Kodi eine Datenbank. In diesem Beispiel kann man mit Rechtsklick auf das Wechsellaufwerk den "Inhalt festlegen". Dabei kann man dann unter "Filme", "Serien" oder "Musikvideos" wählen und mehrere Optionen festlegen.

Für Netzwerklaufwerke gibt es unter "Dateien" die Option "Videos hinzufügen". Dort kann man Pfad und Inhalt festlegen.

<figure class="forth" style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/mediencenter/kodi_usb_inhalt_festlegen_filme_small.jpg" />
	<figcaption>
	</figcaption>
</figure>

**Wichtig**: In den Einstellungen die Sprache auf Deutsch (de) stellen! Die Filme werden sonst unter englischem Namen in der Datenbank gespeichert.
{: .notice-info}

Ein **Scraper** ist eine Webseite die für Filme, Serien oder sonstigem Details verlinkt. Man kann darüber also Informationen zu seinen Filmen - wie Trailer, allerlei Bilder, Filmhandlung, Bewertungen etc. - sich automatisiert holen. Standardmäßig ist "The Movie Database" ausgewählt.

Rekursives Scannen bedeutet, dass in dem ausgewählten Pfad alle Unterordner, deren Unterordner etc. nach abspielbaren Dateien durchsucht werden. Damit wird dann die Datenbank gefüttert. Bei einer großen Menge von Filmen kann das auch mal eine Weile dauern. Ist aber nur einmalig zu Beginn. Wenn neue Dateien dazu kommen wird in regelmäßigen Abständen aktualisiert.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/mediencenter/kodi_filme_small.jpg" />
	<figcaption>
		Hauptmenü mit zusätzlichem Reiter "Filme".
	</figcaption>
</figure>

Wurde die Datenbank mit den Einträgen gespeist, erscheint das Feld "Filme" im Hauptmenü mit den zuletzt zugefügten Filmen.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/mediencenter/kodi_filme_ansicht_small.jpg" />
	<figcaption>
		Filmdatenbank mit Ansicht "Medieninformationen".
	</figcaption>
</figure>

Geht man direkt auf "Filme" erscheint eine Liste aller Filme der Datenbank. In unseren Fall ist das nur einer. Im Menü Links lässt sich die Art der Ansicht der Liste ändern. Hier habe ich mal die Ansicht "Medieninformationen" gewählt. Man Sieht eine Bewertung, Informationen zum Film und eine Kurzbeschreibung.
Das ist alles das Ergebnis des Scrapers. Wirklich toll!

Sobald man das Video zu ca. 90% gesehen hat, erscheint sogar ein Haken in der Liste. Der Film wird also als "gesehen" markiert. Durch setzen eines Filters findet man dann recht schnell noch nicht gesehene Filme.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/mediencenter/big_buck_bunny_small.png" />
	<figcaption>
		Big Buck Bunny - Blender Foundation | www.blender.org
	</figcaption>
</figure>

Der Raspberry Pi 2 kommt damit ohne Probleme klar. Selbst als ich das noch mit dem Raspberry Pi 1 Version B+ getestet hatte, lief das wie geschmiert. Einzig bei Untertitel war der Vorgänger ab und an ein leicht überfordert.

Das wars auch schon fürs Erste. Den Rest findet man leicht selbst oder mit ein wenig Hilfe des Internets heraus. Wenn ihr auf Probleme bei der Installation stoßt, schreibt einfach einen Kommentar!