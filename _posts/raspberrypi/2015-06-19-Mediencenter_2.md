---
layout: article
title: "Mediencenter mit dem Raspberry Pi - Retrospiele"
date: 2015-06-19
modified: 2015-06-19
author: Christian
categories: raspberrypi
share: true
excerpt: "Der Mini-Computer für Filme, Musik, Serien und Spiele."
tags: [raspberrypi, movies, music, games]
toc: true
comments: true
image:
  feature: 
  teaser: raspberrypi/mediencenter/mediencenter_teaser.png
---


<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/mediencenter/super_mario_SNES_screen.png" />
</figure>

Beim letzten [Mal](../Mediencenter){:target="_blank"} habe ich vorgestellt, wie man Filme, Musik und Serien mit dem Mini-PC Raspberry Pi abspielt. Seit kurzem spiele ich damit auch Konsolenspiele wie Super Mario, Final Fantasy oder Sonic.
Wie man das mit dem eingerichteten OpenELEC auf der Raspberry Pi macht, geh ich hier mal Schritt für Schritt durch.

Zu erst holen wir uns das Plugin "RetroArch". Dieses Plugin beinhaltet mehr als nur die gängigen Emulatoren[^emulator] für Konsolen die es so gibt. Gerade die Konsolengeneration von Playstation, Nintendo 64 und alle vorherigen sind dabei vertreten. Atari, Sega Megadrive, Sega Genesis, Super Nintendo, Gameboy, Gameboy Advance, etc... die Liste geht immer weiter und erfüllt so ziemlich jeden retro Spielewunsch den es gibt.

[^emulator]: Ein Emulator ist ein Programm, das so tut als wäre es eine Konsole.

Dann richten wir Spiele ein, um diese direkt aus Kodi zu starten. Hier ist natürlich zunächst wichtig wo wir diese Spiele lagern und darauf zugreifen können.

Als letztes richten wir einen Controller ein. Das kann auch gern ein XBOX 360 Controller sein, wobei aber auch jeder andere USB-Controller funktionieren sollte. Es gibt ja sogar Controller, die genau so aussehen wie z.B. SNES Controller. :D Schon irgendwie cool!

Sobald das alles erledigt ist, können wir anfangen zu spielen! Insgesamt sollte das alles nicht mehr als 30min dauern.

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

Nachdem das geschehen ist, muss man nur noch die ROMs hinzufügen. Roms sind die Spieldateien, die das komplette Spiel beinhalten. Soweit ich weiß, darf man ROMs benutzen, wenn man auch das Originalspiel besitzt. Hier gehe ich aber nicht weiter auf das Rechtliche ein und verweise einfach auf eine beliebige Suchmaschine. Den Rest, könnt und sollt ihr selbst entscheiden.

Diese ROMs kann man entweder direkt auf die SD-Karte des Raspberry Pis kopieren (per Filezilla z.B.), per USB-Stick oder -Festplatte an den Pi hängen oder sogar im Netzwerk freigeben und dann über "Samba" zugreifen. Ist hier genauso wie mit Filmen und Musik. Fragen dazu einfach in den Kommentaren.

Um ein Spiel einzurichten, geht im Hauptmenü auf 

**Programme -> Addvanced Launcher -> Default**

und dann auf die Konsole, zu dem das Spiel gehört. Falls diese nicht existiert müsst ihr einen Eintrag hier hinzufügen. Wir erstellen hier aber mal eine Verknüpfung zu einem SNES Spiel. Also ruft das "Rechtsklickmenü" auf SNES auf und wählt 

**Programmstarter bearbeiten -> Erweiterte Einstellungen.**

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/mediencenter/snes_starter.jpg" />
	<figcaption>
		Einstellungen des SNES Programmstarter
	</figcaption>
</figure>

Dort müsstet ihr nur noch das Verzeichnis zu den Dateien und eventuell Dateierweiterungen anpassen. Das Verzeichnis ist natürlich das, wo die ROMs bei euch liegen. Dateierweiterungen bei SNES können *.smc, *.sfc und *.zip sein. Das kann man so angeben: 

{% highlight bash %}
smc|sfc|zip
{% endhighlight %}

Danach verlasst ihr diese Optionen wieder und wählt im Rechtsklickmenü von SNES "Dateien verwalten". Dort könnt ihr automatisch nach allen Spielen innerhalb des Ordners suchen lassen. Hier sollten dann die Spiele gefunden worden sein.

Achtung ab hier solltet ihr eine Tastatur am Raspberry Pi angeschlossen haben!
{: .notice-info} 

Wählt nun einfach ein Spiel aus und startet es.

## 4.Schritt: Controller konfigurieren

Habt ihr ein Spiel gestartet, sollte nach kurzer Zeit das Spiel mit Intro beginnen. Mit drücken der F1-Taste auf der Tastatur könnt ihr auf ein Menü zugreifen. Ab da ist eigentlich alles selbsterklärend. Geht in die Controller Einstellungen und legt eure Buttons so wie ihr sie gern hättet. 
Ein paar Hinweise jedoch: Man muss das automatische Zuweisung (automatic binding) der Controller abstellen, da sonst jedes mal die Einstellungen überschrieben werden.

Optional sollte man für den Controller sich auch noch einen Button (linker Analogbutton) für das RetroArch Menü einrichten. Dann kann man das Spiel auch wieder verlassen und kommt direkt wieder zu Kodi.

Beim XBOX 360 Controller blinkt derzeit leider dauerhaft die LEDs. Das kommt daher, dass unter OpenELEC nicht die korrekten Treiber installiert sind. Anscheinend wird sich das auch so schnell nicht ändern. Sobald ich was neues höre, schreibe ichs hier rein.

## 5.Schritt: Spielen!

Habt ihr all das geschafft, solltet ihr nun ohne Probleme spielen können. Praktisch bei Emulatoren ist das Speichern und Laden von Spielständen. Egal wo ihr gerade seid, könnt ihr das Spiel wie einen Screenshot speichern und von dort aus weitermachen. Stundenlang nach einem Speicherpunkt zu suchen war früher vielleicht noch in, heute aber nicht mehr.