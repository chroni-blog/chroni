---
layout: article
title: "Homeautomation mit dem Raspberry Pi - Teil 2"
date: 2015-07-09
modified: 2015-07-09
author: Christian
categories: raspberrypi
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
		Ein Beispiel eines fertigen Moduls. Hängt bei mir direkt oben in der Ecke an einem Fenster.
	</figcaption>
</figure>

Mir war das wichtigste an dem Modul, dass ich mehrere unterschiedliche Sensoren anbinden kann. Die Sensoren sollen z.B. die Temperatur und die Feuchtigkeit messen. Ich hab mich dafür entschieden zusätzlich noch einen Fensterkontaktsensor mit anzubauen. So weiß ich dann zusätzlich ob gerade das Fenster in dem Raum offen oder geschlossen ist.

Hier kann ich wieder <a href="http://nathan.chantrell.net/">Nathan Chantrell</a> danken, weil er die meisten Module schon getestet, den Code darauf abgestimmt und frei zur Verfügung (Open Source) gestellt hat. Dadurch hatte ich selbst kaum noch Arbeit mit der Suche nach passenden Modulen.

## Die Komponenten

Eine Zusammenstellung des Moduls kann also so aussehen:

| Bauteil                  | Bezeichnung    | Kosten pro Modul |
|:-------------------------|:---------------|:-----------------|
| Leiterplatte             | PCB TinyTx3    | 0,99 €           |
| Funkmodul                | RFM12B  433Mhz | 3,85 €           |
| Steuereinheit            | ATTINY84A      | 2,05 €           |
| Temp/Feuchtigkeitssensor | DHT22          | 3,99 €           |
| Fensterkontaktsensor     | MC38           | 1,99 €           |
| Batteriehalter           | 2xAA (R6)      | 1,39 €           |
| Gehäuse                  | ---            | 2,99 €           |
|:-------------------------|:---------------|:-----------------|
| **Gesamt**               |                | **17,25 €**      |

Alle Komponenten findet man leicht auf Ebay oder Amazon. Preise können stark schwanken, weshalb es ratsam ist etwas länger zu suchen und eventuell gleich mehrere Komponenten zu kaufen um sich Versandkosten zu sparen.

**Ein komplettes Funkmodul mit Temperatur und Feuchtigkeitssensor (DHT22) und einem Fensterkontaktsensor kostet demnach ca. 17,25€ (zzgl. Versand)**. Dazu braucht man dann noch ein bisschen Draht für die Antenne, jeweils 2 100k&#8486; Widerstände und 2xAA Batterien. Um den Programmcode auf das Modul zu bekommen, fallen eventuell noch weitere Kosten an. Beschreibe ich im nächsten Blogeintrag. Für unsere Basisstation, den Raspberry Pi brauchen wir zusätzlich einen RFM2Pi. Den gibts bei <a href="https://harizanov.com/shop/">Martin Harizanov</a> für 16€ im Internet zu kaufen.

Würde man sich ein ähnliche Module von z.B. HomeMatic kaufen, kosten diese schon 80€. Die Basisstation liegt bei ca. 100€.

Nachfolgend stell ich alle wichtigen Komponenten dar und beschreibe kurz wozu man die braucht.

#### Leiterplatte (PCB TinyTx3)

Die TinyTx3 Platine hab ich mir bei <a href="http://www.seeedstudio.com/service/index.php?r=pcb">Seedstudio</a> bestellt. Dazu braucht ihr natürlich die <a href="http://nathan.chantrell.net/downloads/arduino/tinytx3/tinytx3_gerbers.zip">Gerberdaten/Bauplan</a> von <a href="http://nathan.chantrell.net/">Nathan Chantrell</a>. Ein 10er Pack kostet hier 10$. Der Versand und die Herstellung dauert jedoch ein paar Wochen.

<figure style="text-align: center">
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/pcb.jpg">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/pcb_small.jpg">
	</a>
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/pcbback.jpg">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/pcbback_small.jpg">
	</a>
	<figcaption>
		Leiterplatte TinyTx3
	</figcaption>
</figure>

Dieses Ding ist schon echt verdammt klein. Da braucht man schon ein ruhiges Händchen beim Löten. Zum Glück sind da alle wichtigen Informationen aufgedruckt. Auf der Rückseite gibt es ein kleines Feld auf der man die Node ID Nummer schreiben kann. Man sollte auf jeden Fall alle Module durchnummerieren! Das wird dann auch wieder bei der Programmierung wichtig.

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


## Bau des Moduls

Alles was jetzt fehlt, ist das Löten des Moduls. Gar nicht so leicht saubere Lötstellen bei dieser Größe hinzubekommen. Wie man die Module anbringt, kann man zum einen durch die Markierungen auf der Leiterplatte erkennen oder man orientiert sich an dem folgenden Bild.

<figure style="text-align: center">
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/bauplan_tinytx3.png">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/bauplan_tinytx3_small.png">
	</a>
	<figcaption>
		Bauplan der Komponenten.
	</figcaption>
</figure>

Ein paar Fotos dazu: 

<figure class="fourth" style="text-align: center">
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/bau_1.jpg">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/bau_1_small.jpg">
	</a>
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/bau_2.jpg">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/bau_2_small.jpg">
	</a>
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/bau_3.jpg">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/bau_3_small.jpg">
	</a>
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/bau_4.jpg">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/bau_4_small.jpg">
	</a>
	<figcaption>
		Bilder während des Baus des Moduls.
	</figcaption>
</figure>

Am besten fängt man mit dem ATTiny84A an (linkes Bild). Die Lötstellen müssen hier so perfekt wie möglich sein! Wenn man später den Code aufspielt gibt es sonst nur Probleme! Als nächstes kann man das Funkmodul (RFM12B) anbringen. Das wären dann die zwei wichtigsten Komponenten.

Im zweiten Bild sieht man die Kontakte der Kabel vom Batteriehalter. Hierüber läuft dann der Strom der Batterien. 

Das dritte Bild zeigt eine viel zu große Antenne. Diese sollte ungefähr 0,6mm Durchmesser und bei 433Mhz eine Länge von ca. 16,5cm haben. Hier ist auch der DHT22 schon angebracht.

Im vierten Bild ist alles bis auf der Fensterkontaktsensor angebracht. Hier sieht man nochmal genau, wo der DHT angelötet werden muss. Der zweite Kontakt ist nach hinten gebogen. Den brauchen wir gar nicht.
Die Antenne ist hier zu einer Spirale verdreht. Leider war der Empfang in dem Gehäuse so nicht gut genug in meiner Wohnung. Das Signal musste öfter geschickt werden, bis es als vollständig übertragen erkannt wurde.Später hab ich die Antenne wieder gerade gezogen und aus dem Gehäuse zeigen lassen. Damit reduzierten sich die fehlgeschlagenen Übertragungen.

Sobald alles fertig ist, kommen wir zum Programmcode und wie man den auf den ATTiny bekommt. Das aber dann im nächsten Teil.