---
layout: article
title: "Homeautomation mit dem Raspberry Pi - Teil 2"
date: 2015-07-07
modified: 2015-07-07
author: Christian
categories: unpublished
share: true
excerpt: "Temperaturmessung zum Selbstbauen mit dem Raspberry Pi - Bauen der Funkmodule"
tags: [raspberrypi, homeautomation]
toc: true
comments: true
image:
  feature: 
  teaser: raspberrypi/homeautomation/homeautomation_teaser.png
---

Im ersten Teil dieser Serie, hab ich dene groben [Plan und die Übersicht](../HomeAutomation){:target="_blank"} beschrieben. Hier erklär ich, wie ich die Sendermodule der Hausautomation gebaut hab und zeige was sich damit alles anstellen lässt.
Nun geh ich auf den Bau eines Moduls ein. 

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
		Ein Beispiel eines fertigen Moduls
	</figcaption>
</figure>

Das wichtigste an dem Modul ist, dass man mehrere unterschiedliche Sensoren anbinden können soll. Die Sensoren sollen z.B. die Temperatur und die Feuchtigkeit messen. Ich hab mich dafür entschieden zusätzlich noch einen Fensterkontaktsensor mit anzubauen. So weiß ich dann zusätzlich ob gerade das Fenster in dem Raum offen oder geschlossen ist.

Hier kann ich wieder <a href="http://nathan.chantrell.net/">Nathan Chantrell</a> danken, weil er die meisten Module schon getestet, den Code darauf abgestimmt und frei zur Verfügung gestellt hat. Dadurch hatte ich selbst kaum noch Arbeit mit der Suche nach passenden Modulen.

Eine Zusammenstellung des Moduls kann also so aussehen:

| Bauteil                  | Bezeichnung    | Kosten pro Modul |
|:-------------------------|:---------------|:-----------------|
| Leiterplatte             | PCB TinyTx3    | 0,99 €           |
| Funkmodul                | RFM12B  433Mhz | 3,85 €           |
| Steuereinheit            | ATTINY 84 A    | 2,05 €           |
| Temp/Feuchtigkeitssensor | DHT22          | 3,99 €           |
| Fensterkontaktsensor     | MC38           | 1,99 €           |
| Batteriehalter           | 2xAA (R6)      | 1,39 €           |
| Gehäuse                  | ---            | 2,99 €           |
|:-------------------------|:---------------|:-----------------|
| **Gesamt**               |                | **17,25 €**      |

**Ein komplettes Funkmodul mit Temperatur und Feuchtigkeitssensor (DHT22) und einem Fensterkontaktsensor kostet demnach ca. 17,25€ (zzgl. Versand)**. Dazu braucht man dann noch ein bisschen Draht für die Antenne, jeweils 2 100k&#8486; Widerstände und 2xAA Batterien.

Würde man sich ein ähnliche Module von z.B. HomeMatic kaufen, kosten diese schon 80€.


#### Leiterplatte (PCB TinyTx3)

Die TinyTx3 Platine hab ich mir bei <a href="http://www.seeedstudio.com/service/index.php?r=pcb">Seedstudio</a> bestellt. Dazu braucht ihr natürlich die <a href="http://nathan.chantrell.net/downloads/arduino/tinytx3/tinytx3_gerbers.zip">Gerberdaten/Bauplan</a>. Ein 10er Pack kostet hier 10$. Der Versand und die Herstellung dauert jedoch ein paar Wochen.

<figure style="text-align: center">
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/pcb.jpg">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/pcb_small.jpg">
	</a>
	<figcaption>
		Leiterplatte TinyTx3
	</figcaption>
</figure>

Dieses Ding ist schon echt verdammt klein. Da braucht man schon ein ruhiges Händchen beim Löten. Zum Glück sind da alle wichtigen Informationen aufgedruckt.

#### Funkmodul (RFM12b)

Der RFM12b wird direkt auf die Leiterplatte gelötet. Man kann sich dabei für 433Mhz oder 868Mhz entscheiden. Ich hatte mich preislich für 433Mhz entschieden.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/homeautomation/RFM12B.jpg">
	<figcaption>
		Das Funkmodul. Durch dieses Bauteil können Daten per Funk übertragen werden.
	</figcaption>
</figure>

#### Steuereinheit (ATTINY 84 A)

Das ist unser Mini-Rechner. Sobald Strom anliegt, führt er den Code aus, der auf ihn geschrieben wurde. Er kann die Daten der Sensoren aufnehmen und dann über das Funkmodul losschicken.

<figure style="text-align: center">
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/ATTINY84A.jpg">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/ATTINY84A_small.jpg">
	</a>
	<figcaption>
		Die Steuereinheit. Hier kann Programmcode aufgespielt und ausgeführt werden.
	</figcaption>
</figure>

Wie man Programmcode auf den ATTiny bekommt, beschreibe ich im nächsten Teil des Blogs.

#### Temperatur und Feuchtigkeitssensor (DHT22)

Der DHT22 erfasst die räumliche Temperatur und Feuchtigkeit. 

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/homeautomation/dht22.jpg">
	<figcaption>
		Ein Temperatur und Feuchtigkeitssensor.
	</figcaption>
</figure>

#### Fensterkontaktsensor (MC38)

Sobald beide Teile des MC38 nah bei einander sind (ab ca. 1cm Distanz) fließt Strom. Wenn beide von einander weiter entfernt sind, fließt kein Strom. Somit kann man z.B. erfassen ob eine Tür oder ein Fenster geschlossen oder offen ist.

<figure class="half" style="text-align: center">
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/MC38.jpg">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/MC38_small.jpg">
	</a>
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/MC38_1.jpg">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/MC38_1_small.jpg">
	</a>
	<figcaption>
		Erkennt ob ein/e Tür/Fenster offen oder geschlossen ist.
	</figcaption>
</figure>



### Abbildung mit Komponenten

Jedes Modul besteht dabei aus einer Platine, einer Steuereinheit, einem Funksendemodul, Batterien und ein oder mehrere Sensoren. Um Strom zu sparen, sendet man nicht andauernd Daten über Funk zur Basisstation. Das würde bei weitem zu viel Strom kosten und würde uns auch nicht sinnvollere Informationen liefern. Temperatur und Feuchtigkeit ändern sich ja schließlich nicht innerhalb weniger Sekunden. 

Auf die Steuereinheit selbst kann man direkt Programmcode kopieren und dann immer wieder ausführen lassen. Hier kann man also selbst festlegen, wie oft man Daten ausliest und schickt. Die Informationen selbst, die in der Nachricht an die Basisstation (den Raspberry Pi) stehen, können natürlich auch selbst festgelegt werden. Ich selbst lasse jedes Modul alle 2 Minuten die Daten an den Raspberry Pi weiterschicken.

Sensoren ermitteln bei "Anfrage" der Steuereinheit die Messdaten an diese wieder zurück. Auch diese werden nur zeitlich vor einem Datenaustausch angesprochen und verbrauchen ansonsten wenig bis keinen Strom. 

