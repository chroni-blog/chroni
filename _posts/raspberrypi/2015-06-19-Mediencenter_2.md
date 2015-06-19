---
layout: article
title: "Mediencenter mit dem Raspberry Pi - Retrospiele"
date: 2015-06-19
modified: 2015-06-19
author: Christian
categories: unpublished
share: true
excerpt: "Der Mini-Computer für Filme, Musik, Serien und Spiele."
tags: [raspberrypi, movies, music, games]
toc: true
comments: true
image:
  feature: 
  teaser: raspberrypi/mediencenter/mediencenter_teaser.png
---

Beim letzten [Mal](../Mediencenter){:target="_blank"} habe ich vorgestellt, wie man Filme, Musik und Serien mit dem Mini-PC Raspberry Pi abspielt. Seit kurzem spiele ich damit auch Konsolenspiele wie Super Mario, Final Fantasy oder Sonic.
Wie man das mit dem eingerichteten OpenELEC auf der Raspberry Pi macht, geh ich hier mal Schritt für Schritt durch.

Zu erst holen wir uns das Plugin "RetroArch". Dieses Plugin beinhaltet mehr als nur die gängigen Emulatoren[^emulator] für Konsolen die es so gibt. Gerade die Konsolengeneration von Playstation, Nintendo 64 und alle vorherigen sind dabei vertreten. Atari, Sega Megadrive, Sega Genesis, Super Nintendo, Gameboy, Gameboy Advance, etc... die Liste geht immer weiter und erfüllt so ziemlich jeden retro Spielewunsch den es gibt.

[^emulator]: Ein Emulator ist ein Programm, das so tut als wäre es eine Konsole.

Zu Beginn befinden wir uns im Hauptmenü von Kodi.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/mediencenter/kodi_small.jpg" />
	<figcaption>
		Hauptmenü bei fertig eingerichtetem OpenELEC.
	</figcaption>
</figure>

Zuerst aber müssen wir uns mit einem PC an dem Raspberry Pi einloggen.

## 1.Schritt: Einloggen auf dem Raspberry Pi mit einem PC über SSH

Um per SSH[^ssh] sich mit dem Rechner zu verbinden, kann man bei einem Windows PC das Programm <a href="http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html">Putty</a> nehmen. Dazu muss der Raspberry Pi mit dem Rechner im LAN verbunden sein.

[^ssh]: SSH ist ein Protokoll, über welches man relativ direkt und sicher nutzen kann um mit anderen Rechnern zu kommunizieren.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/mediencenter/putty.PNG" />
	<figcaption>
		Einstellungen bei Putty. Ich selbst habe zwei Raspberry Pis und habe beiden einen Listeneintrag gegeben. Ist aber nicht zwingend notwendig.
	</figcaption>
</figure>

Die IP-Adresse des Raspberry Pi könnt ihr in Kodi unter System -> Systeminfo -> Info nachsehen. Diese muss natürlich dann in Putty eingegeben werden. Sobald ihr euch verbunden habt, wird nach einem Passwort und einem Benutzernamen gefragt. Gebt dabei den Benutzer "root" und das Passwort "openelec" ein (Standardeinstellungen). Bei mir sieht das dann so aus:

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/mediencenter/putty_login.PNG" />
	<figcaption>
		Einstellungen bei Putty.
	</figcaption>
</figure>

## 2.Schritt: Installieren des Plugins

Um nun RetroArch samt dem AdvancedLauncher (ermöglicht einfachereres Starten von Spielen) zu installieren gebt folgende Befehle nacheinander ein:

{% highlight bash %}
wget http://misapuntesde.com/res/AdvLauncher_uLySeSS.zip
unzip AdvLauncher_uLySeSS.zip -d /
rm AdvLauncher_uLySeSS.zip
killall -9 kodi.bin
{% endhighlight %}

Diese simple Installation haben wir <a href="http://misapuntesde.com/post.php?id=502">mezzo</a> zu verdanken. Danach startet sich der Pi kurz neu.


## 3.Schritt: Spiele hinzufügen

Nachdem das geschehen ist, muss man nur noch die ROMs hinzufügen. Roms sind die Spieldateien, die das komplette Spiel beinhalten. Hier gehe ich nicht weiter auf rechtliches ein und verweise einfach auf eine beliebige Suchmaschine. Soweit ich weiß, darf man ROMs benutzen, wenn man auch das Originalspiel besitzt.

Diese ROMs kann man entweder direkt auf die SD-Karte des Raspberry Pis kopieren (per Filezilla z.B.), per USB-Stick oder -Festplatte an den Pi hängen oder sogar im Netzwerk freigeben und dann über "Samba" zugreifen. Ist hier genauso wie mit Filmen und Musik. Fragen dazu einfach in den Kommentaren.

## 4.Schritt: Controller konfigurieren

Zunächst sollte man eine Tastatur am Pi anschliessen. Startet man ein Spiel, kann man mit F1 auf ein Menü zugreifen. Ab da ist eigentlich alles selbsterklärend. Ein paar Hinweise jedoch: Man muss das automatische binding der Controller abstellen, da sonst jedes mal die Einstellungen überschrieben werden.

Optional sollte man für den Controller sich auch noch einen Button für das RetroArch Menü einrichten. Dann kann man das Spiel auch wieder verlassen und kommt direkt wieder zu Kodi.