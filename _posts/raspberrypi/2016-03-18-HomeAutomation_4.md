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
Der dritte [Teil](../HomeAutomation_3){:target="_blank"} hat gezeigt wie man Code auf das Modul schreibt. 

Jetzt wird das Empfangsmodul und der Raspberry Pi in Betrieb genommen. Ich nutze hier übrigens einen Raspberry Pi 1. Neuere Versionen sollten aber genauso funktionieren und die selben Schritte enthalten.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/homeautomation/install_raspbian_and_communicate.png">
</figure>

## Raspbian installieren

Im [Mediencenter-Artikel](../Mediencenter){:target="_blank"} wurde das System direkt über ein Image installiert. Jetzt will ich mal eine Alternative mit <a href="https://www.raspberrypi.org/downloads/noobs/">NOOBS</a> zeigen. Hier läd man sich entweder NOOBS oder NOOBS Lite herunter. Ich hab einfach mal die Lite Version genommen. Diese entpackt man einfach direkt auf die formatierte und leere SD-Karte. Ab damit in den Raspberry Pi und booten lassen!

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/homeautomation/noobs.png">
	<figcaption>
		Auswahlmenü in NOOBS. Hat sich seitdem kaum verändert.
	</figcaption>
</figure>


Bei der NOOBS Lite Variante muss das Betriebssystem zuerst noch heruntergeladen werden. Daher braucht man hier einen Netzwerkzugang zum LAN über Ethernet-Kabel. Anfangs braucht man auch noch einen Bildschirm (TV oder Monitor) und eine Tastatur oder eine Maus. Sobald der Pi hochgefahren ist, kann man sein Betriebssystem wählen. Hier wählen wir "Raspbian" aus (mit "Leertaste") und installieren es (Shortcut: "i"). Ab jetzt kann man sich eine Weile zurücklehnen und dem Installationsbalken zuschauen wie er sich langsam füllt.

Nachdem die Installation beendet ist, bootet der Pi in eine vorinstallierte GUI. Diese brauchen wir jedoch nicht. Viel praktischer ist es von einem Rechner, einem Tablett oder sonst einem Gerät per SSH zuzugreifen und alles weitere Remote zu steuern. Zunächst aber die Grundeinstellungen (Tastatur, Sprache, etc.).
Wir öffnen also ein Terminal unter "Menu" -> "Accessories" -> "Terminal" und starten
{% highlight bash %}
	sudo raspi-config
{% endhighlight %}

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/homeautomation/raspi-config-configuration-rasbian.png">
	<figcaption>
		Raspi-config Menü. Hier können Grundeinstellungen für den RPi vorgenommen werden.
	</figcaption>
</figure>

In den "International Options" richten wir Sprache, Zeitzone und Keyboard Layout ein. Das sollte alles recht selbsterklärend ablaufen. 

* In "Locale" wählt man am besten "de_DE.UTF-8 UTF8". Default lässt man auf "en_GB.UTF-8 UTF8".
* In "Timezone" wählt man "Europe" und dann "Berlin". Keyboard dann "Generic 105-key (Intl) PC".
* Bei Keyboard Layout "Other" und "German", "German". Den Rest lass ich immer auf den Standardeinstellungen. 

Eine wichtige Einstellung ist das Deaktivieren des Zugriffs über den seriellen Port. Dieser muss für das Modul RFM12Pi frei bleiben. Daher wählen wir unter SerialPort -> No

Ab jetzt schalten wir auch das Booten in die GUI aus. Unter "Boot Options" wählen wir "Console". Als nächstes beenden wir raspi-config über "Finish" und bestätigen einen Neustart.
Ab jetzt kann man sich mit dem Login "pi" und Passwort "raspberry" einloggen.


## WLAN einrichten (optional)

Falls man WLAN nutzen will muss man dieses natürlich vorher einrichten. Ist der Raspberry Pi dauerhaft im LAN per Kabel, kann man diesen Abschnitt überspringen.
Kennt man seine SSID nicht auswendig, kann man alle erreichbaren Netzwerke mit "sudo iwlist wlan0 scan" anzeigen lassen.

Zunächst rufen wir die WLAN konfigurations datei in nano auf:
{% highlight bash %}
	sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
{% endhighlight %}

Hier fügt man die Daten des WLAN Netzwerks einfach darunter ein. 
Z.B. so:
{% highlight bash %}
	network={
		ssid="DeineSSID"
		psk="DeinWLANPasswort"
	}
{% endhighlight %}

Sobald das erledigt ist (Nano: Speichern mit STRG+O, Beenden mit STRG+X), startet man das WLAN-Netzwerk neu mit
{% highlight bash %}
	sudo ifdown wlan0
	sudo ifup wlan0
{% endhighlight %}
und prüft mit "ifconfig wlan0" ob eine gültige Netzwerk-Adresse (z.B. 192.168.x.x) zugewiesen wurde.


## Zugriff auf den Raspberry Pi mit SSH

Um auf den Raspberry Pi aus dem Netzwerk zugreifen zu können brauchen wir einen SSH-Client wie z.B. <a href="http://www.putty.org/">Putty</a>. Hier muss man nur noch den Hostnamen order die IP-Adresse eingeben und eine Sitzung mit "Open" öffnen.

Wir nutzen den Hostnamen, da die IP-Adresse durch den DHCP-Dienst vom Router vergeben wird und sich dadurch ändern kann. Der Hostname ist per default "raspberrypi", lässt sich jedoch in "/etc/hostname" und "/etc/hosts" ändern (jeweils wieder mit nano öffnen, Neustart mit "reboot" nicht vergessen!).

Beim ersten Zugriff erscheint eine Warnung. Diese bestätigen wir einfach und fahren mit dem gewohnten Login fort. Ab jetzt haben wir Zugriff auf den Raspberry Pi aus dem Netzwerk und können ihn in irgendeinen Schrank ohne Monitor und Tastatur stecken (Netzwerk natürlich trotzdem nötig).

## Installieren von Node-RED



{% highlight bash %}
sudo nano /boot/config.txt
{% endhighlight %}

Am Ende der Datei dann folgendes einfügen um den DeviceTree zu deaktivieren.

{% highlight bash %}
device_tree=
{% endhighlight %}

Node-RED lässt sich direkt mit folgenden Befehlen installieren:
{% highlight bash %}
	sudo apt-get update
	sudo apt-get upgrade
	sudo apt-get install python-dev python-rpi.gpio
	sudo apt-get install nodered
	sudo systemctl enable nodered.service
{% endhighlight %}

Der letzte Befehl startet Node-RED automatisch nach einem Neustart. Das probieren wir auch am besten gleich aus. Nach einem "sudo reboot" prüfen wir ob alles funktioniert hat. Im Browser unter "http://raspberrypi:1880" sollte nun Node-RED starten.

<!-- Noobs Lite herunterladen, auf formatierte SD Karte kopieren.
 SD Karte in RPi stecken
 booten
 Netzwerkkabel (bei Lite) benötigt!
 Raspbian auswählen (Leertaste), installieren (i), warten 

 Internationational -->

