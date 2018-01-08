---
layout: article
title: "Homeautomation mit dem Raspberry Pi - Teil 4"
date: 2016-03-18
modified: 2016-03-21
author: Christian
categories: raspberrypi
share: true
excerpt: "Temperaturmessung zum Selbstbauen mit dem Raspberry Pi - Einrichten des RPis"
tags: [raspberrypi, homeautomation]
toc: true
comments: true
image:
  feature: 
  teaser: raspberrypi/homeautomation/homeautomation_teaser.png
---

In [Teil 1](../HomeAutomation){:target="_blank"} der Serie hab ich einen groben Plan und die Übersicht beschrieben, wobei [Teil 2](../HomeAutomation_2){:target="_blank"} den Aufbau der kleinen Sendemodule beschreibt. 
Im dritten [Teil](../HomeAutomation_3){:target="_blank"} steht, wie man Code auf den ATTiny schreibt. 

Jetzt wird das Empfangsmodul und der Raspberry Pi in Betrieb genommen. Ich nutze hier übrigens einen Raspberry Pi 1. Neuere Versionen sollten aber genauso funktionieren und die selben Schritte enthalten.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/homeautomation/install_raspbian_and_communicate.png">
</figure>


<figure class="half" style="text-align: center">
    <a href="{{ site.url }}/images/raspberrypi/homeautomation/empfaenger1.jpg">
        <img src="{{ site.url }}/images/raspberrypi/homeautomation/empfaenger1_small.jpg">
    </a>
    <a href="{{ site.url }}/images/raspberrypi/homeautomation/empfaenger2.jpg">
        <img src="{{ site.url }}/images/raspberrypi/homeautomation/empfaenger2_small.jpg">
    </a>
    <figcaption>
        So sieht der Empfänger auf dem Raspberry aus.
    </figcaption>
</figure>

## Raspbian installieren

Im [Mediencenter-Artikel](../Mediencenter){:target="_blank"} wurde das System direkt über ein Image installiert. Jetzt will ich mal eine Alternative mit <a href="https://www.raspberrypi.org/downloads/noobs/">NOOBS</a> zeigen. Hier läd man sich entweder NOOBS oder NOOBS Lite herunter. Ich hab einfach mal die Lite Version genommen. Diese entpackt man einfach direkt auf die formatierte und leere SD-Karte. Ab damit in den Raspberry Pi und booten lassen!

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/homeautomation/noobs.png">
	<figcaption>
		Auswahlmenü in NOOBS. Hat sich seitdem kaum verändert.
	</figcaption>
</figure>


Bei der NOOBS Lite Variante muss das Betriebssystem zuerst noch heruntergeladen werden. Daher braucht man hier einen Netzwerkzugang zum LAN über Ethernet-Kabel. Anfangs braucht man auch noch einen Bildschirm (TV oder Monitor) und eine Tastatur oder eine Maus. Sobald der Pi hochgefahren ist, kann man sein Betriebssystem wählen. Hier wählen wir `Raspbian` (`Jessie`) aus (mit `Leertaste`) und installieren es (Shortcut: `i`). Ab jetzt kann man sich eine Weile zurücklehnen und dem Installationsbalken zuschauen wie er sich langsam füllt.

Nachdem die Installation beendet ist, bootet der Pi in eine vorinstallierte GUI. Diese brauchen wir jedoch nicht. Auch wenn man durch Windows eventuell an so etwas gewohnt ist, lässt sich gerade auf dem Raspberry Pi vieles einfacher über Kommandozeile regeln. Praktisch zudem, dass man von einem Rechner, einem Tablett oder sonst einem Gerät per SSH zuzugreifen kann. Zunächst aber die Grundeinstellungen (Tastatur, Sprache, etc.).
Um sich gleich schon mal daran zu gewöhnen öffnen wir also ein Terminal unter `Menu` -> `Accessories` -> `Terminal` und starten
{% highlight bash %}
	sudo raspi-config
{% endhighlight %}

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/homeautomation/raspi-config-configuration-rasbian.png">
	<figcaption>
		Raspi-config Menü. Hier können Grundeinstellungen für den RPi vorgenommen werden.
	</figcaption>
</figure>

In den `International Options` richten wir Sprache, Zeitzone und Keyboard Layout ein. Das sollte alles recht selbsterklärend ablaufen. Trotzdem hier alles wichtige zusammengefasst:

* In `Locale` wählt man am besten `de_DE.UTF-8 UTF8`. Default lässt man auf `en_GB.UTF-8 UTF8`.
* In `Timezone` wählt man `Europe` und dann `Berlin`. Keyboard dann `Generic 105-key (Intl) PC`.
* Bei Keyboard Layout `Other` und `German`, `German`. Den Rest einfach auf den Standardeinstellungen lassen.

Eine viel wichtigere Einstellung ist das Deaktivieren des externen Zugriffs über den seriellen Port. Dieser muss für den RFM12Pi frei bleiben, da der Port sonst belegt ist und nicht von dem Modul genutzt werden kann. Deswegen wählen wir unter `Advanced Options` -> `Serial` -> `No`.

Ab jetzt schalten wir auch das Booten in die GUI aus. Also wählen wir unter `Boot Options` -> `Console`. 
Zu guter Letzt beenden wir raspi-config über `Finish` und bestätigen einen Neustart.
Ab jetzt müssen wir uns mit dem Login `pi` und Passwort `raspberry` einloggen.

Am besten gleich aus Sicherheitsgründen mit `passwd` ein anderes Passwort vergeben!
{: .notice-info}







## WLAN einrichten (optional)

Falls man WLAN nutzen will, muss man dieses natürlich vorher einrichten. Ist der Raspberry Pi dauerhaft im LAN per Kabel, kann man diesen Abschnitt überspringen.
Kennt man die SSID seines WLAN-Netzes nicht auswendig, kann man alle erreichbaren Netzwerke mit `sudo iwlist wlan0 scan` anzeigen lassen. Darunter muss man dann nur noch seine eigene finden.

Danach rufen wir die WLAN konfigurations datei in nano auf:
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

Sobald das erledigt ist (nano: Speichern mit STRG+O, Beenden mit STRG+X), startet man das WLAN-Netzwerk neu mit
{% highlight bash %}
	sudo ifdown wlan0
	sudo ifup wlan0
{% endhighlight %}
und prüft mit `ifconfig wlan0` ob eine gültige Netzwerk-Adresse (z.B. 192.168.x.x) zugewiesen wurde.






## Zugriff auf den Raspberry Pi mit SSH

Um auf den Raspberry Pi aus dem Netzwerk zugreifen zu können brauchen wir einen SSH-Client wie z.B. <a href="http://www.putty.org/">Putty</a>. Hat man diesen heruntergeladen und gestartet muss man nur noch den Hostnamen oder die IP-Adresse eingeben und eine Sitzung mit `Open` öffnen.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/homeautomation/putty.png">
	<figcaption>
		Das Programm "Putty".
	</figcaption>
</figure>

Wir nutzen den Hostnamen, da die IP-Adresse durch den DHCP-Dienst vom Router vergeben wird und sich dadurch im Laufe der Zeit auch mal ändern kann. Der Hostname ist per default `raspberrypi`. Beim ersten Zugriff mit Putty erscheint eine Warnung. Diese bestätigen wir und fahren mit dem gewohnten Login fort. Ab jetzt haben wir Zugriff auf den Raspberry Pi aus dem Netzwerk und können ihn in irgendeinen Schrank ohne Monitor und Tastatur stecken (Netzwerk natürlich trotzdem nötig).



#### Eigenen Hostnamen setzen

Der Hostname lässt sich aber auch frei wählen. Ich hab ihn bei mir auf `home` geändert und werde auch diesen Hostnamen ab jetzt hier verwenden. Dafür muss man folgendes tun:

* `sudo hostname -b <neuer_Hostname>` 
* In den beiden Dateien, `/etc/hosts` und `/etc/hostname`, `raspberrypi` mit dem neuen Namen ersetzen.
* In `/etc/samba/smb.conf` einen Wert wie folgt ändern:
{% highlight bash %}
	dns proxy = yes
{% endhighlight %}

Damit ist dann der Hostname im Netzwerk auffindbar.







## Installieren von Node-RED

Node-RED ist ein Programm um ... nein ich werde dieses *hust* gruselige Wort `IOT` nicht ausschreiben ... alle möglichen kleinen Module zu verknüpfen und dem Ganzen eine Logik zu geben. Sprich: Hier kommen die Signale an, werden interpretiert und dann (im nächsten Kapitel) in eine Datenbank geschrieben. Nun aber zuerst die Installation.

Zu aller erst machen wir mal ein Update des Betriebssystems mit:
{% highlight bash %}
	sudo apt-get update
	sudo apt-get upgrade
{% endhighlight %}

Das kann schon einmal eine Weile dauern. Hier werden alle Bibliotheken, welche installiert sind, auf den neuesten Stand gebracht.

Nutzt man die ältere Version `Raspbian Wheezy`, muss man die Installation komplett anders vornehmen. In dem Fall einfach dieser Anleitung <a href="http://nodered.org/docs/hardware/raspberrypi#manual-install">**hier**</a> folgen.
{: .notice-info}

Node-RED lässt sich direkt mit folgenden Befehlen (wenn man `Raspbian Jessie` verwendet) installieren:
{% highlight bash %}
	sudo apt-get install python-dev python-rpi.gpio
	sudo apt-get install nodered
	sudo systemctl enable nodered.service
{% endhighlight %}

Der letzte Befehl startet Node-RED automatisch nach einem Neustart. Das probieren wir auch am besten gleich aus. Nach einem `sudo reboot` prüfen wir ob alles funktioniert hat. Hat der Pi den Hostnamen `home`wie bei mir, kann man im Browser unter <a href="http://home:1880">http://home:1880</a> die Node-RED Oberfläche starten.

Die Oberfläche ist in drei Bereiche geteilt: Links die Übersicht aller vorhandenen Module, in der Mitte das Netzwerk (anfangs leer) und rechts Informationen. Dort wählen wir `Debug`, um alle Debug-Messages zu sehen.


#### Ein Node-RED Netzwerk erstellen

Zu erst erstellen wir durch Drag&Drop ein `input -> serial` Modul. Damit bekommen wir die Signale ins Netzwerk und können diese dann verarbeiten.
Mit einem Doppelklick auf das erstellte Modul und einem Klick auf das Editiericon kommen wir auf dessen Einstellungen.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/homeautomation/Node-RED_serialmodule.png">
	<figcaption>
		Einstellungen für das Serial-Modul.
	</figcaption>
</figure>



Hier stellen wir den SerialPort auf `/dev/ttyAMA0` mit einer Baud Rate von 9600. Den Rest lassen wir wie es ist. Mit `Update` bestätigen.
Als nächstes hängen wir ein Debug-Modul an und hoffen auf die ersten Zeichen unserer Sendemodule. Je nachdem wie oft das Modul sendet, kann das auch mal ein paar Minuten dauern. Wem das zu lang ist: Batterie raus und wieder rein. Dann sendet es sofort.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/homeautomation/Node-RED_initial_signal.PNG">
	<figcaption>
		Das erste Signal in Node-RED ist angekommen. Wer es bis hierher geschafft hat kann sich entspannen. Der Rest ist "easy as pi(e)".
	</figcaption>
</figure>

Kommt wider erwarten kein Signal an, kann das zum einen natürlich am Sendemodul, der Empfangsmodul oder aber auch an der Konfiguration des Raspberry Pis liegen. Als ersten Tipp kann ich hier das Tool `minicom` empfehlen.
Dieses installiert man mit `sudo apt-get install minicom` und wird mit `minicom -b 9600 -o -D /dev/ttyAMA0` gestartet.
Sollte man auch damit nicht herausfinden woran der Fehler liegt: Kommentar schreiben! Hab selbst schon viel Zeit verbracht bis alles ging. Auch das flashen der Firmware kann wunder bewirken!
{: .notice-info}

Ist soweit alles am Laufen, kann man das Signal dekodieren. Dazu legt man ein `function`-Modul an und verbindet es mit dem Serial-Modul von oben (jetzt `/dev/ttyAMA0`).
Dort gibt man folgenden Code an (Für Standard DHT22-Module):

{% highlight javascript %}
msg.payload = msg.payload.trim(); // raw signal

var tokens = msg.payload.split(" ", 66); //RFM2Pi max 66 bytes payload
var outString = [];
var outTopic = null;
var msg2 = null;
var nodeid = tokens.shift(); // gets Node ID

// if nodeid is valid
if (!isNaN(nodeid)){
    nodeid = nodeid & 0x1F; // Strip out additional flags
    outString.push(nodeid);
    outString.push('DHT22');

    // retrieve signal information
    var raw = tokens;
    buf = new Buffer (raw);
    
    outValues = [];
    outValues.push(buf.readInt16LE(0) / 100);   // humidity
    outValues.push(buf.readInt16LE(2) / 1000);  // voltage
    outValues.push(buf.readInt16LE(4) / 100);   // temperature
    
    outString.push(outValues.join(" "));
    
    msg2 = { payload:outString, topic:" "};
}

return msg2;
{% endhighlight %}

Hängt man das Debug-Modul nun an den Ausgang rechts des function-Moduls (hier `parse` genannt), sollten die zukünftigen Signale richtig interpretiert werden.
Ich habe hier noch in den outString den Text "DHT22" eingefügt. Da meine Module untereinander unterschiedliche Dinge können, muss ich zwischen ihnen unterscheiden. Das mache ich anhand der IDs und weise demnach andere Modulnamen zu (DHT22, DHT22_MC38, etc.). Natürlich könnte man das auch direkt in das Signal auf dem ATtiny packen. Werd' ich in Zukunft irgendwann mal machen...

Hat man übrigens den Hostnamen des Pis geändert nachdem man schon ein Netzwerk mit Node-RED erstellt hat (so wie ich), wird ein neues leeres Netzwerk angezeigt. Um das vorherige Netzwerk wieder zu nutzen, kann man in `$home/.node-red/settings.js` den folgenden Wert setzen: `flowfile: 'flows_raspberrypi.json'`. Damit wird unabhängig vom Hostnamen ein fester Dateiname für das Netzwerk verwendet.
{: .notice-info}

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/homeautomation/Node-RED_interpreted_signal.png">
	<figcaption>
		Die Ausgabe eines interpretierten Signals. ID 16 mit 62,6% Luftfeuchtigkeit, 3,044V und 20.2°C.
	</figcaption>
</figure>

Geschafft! Ein erstes lesbares Signal kommt an. Ab hier kann man schon ein wenig herumexperimentieren. Distanzen der Sendemodule testen, Sendezeiten anpassen, usw.
Beim nächsten Teil der Serie Homeautomation mit dem Raspberry Pi legen wir eine Datenbank an, um die ankommenden Signale zu speichern und setzen eine hübsche Weboberfläche auf.
