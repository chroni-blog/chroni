---
layout: article
title: "Homeautomation mit dem Raspberry Pi - Teil 1"
date: 2015-07-07
modified: 2015-07-07
author: Christian
categories: raspberrypi
share: true
excerpt: "Temperaturmessung zum Selbstbauen mit dem Raspberry Pi - Übersicht/Beginn"
tags: [raspberrypi, homeautomation]
toc: true
comments: true
image:
  feature: 
  teaser: raspberrypi/homeautomation/homeautomation_teaser.png
---

Kaum hat man mal ein wenig mehr Erfahrung mit dem Raspberry Pi, kommt man auf allerlei Ideen. Es gibt [Mediencenter](../Mediencenter){:target="_blank"}, Web- und Datenserver, [Spielekonsole](../Mediencenter_2){:target="_blank"}, Aquariensteuerungen, automatische Sprenkleranlagen, uvm.
Hier beschreibe ich mal ein Projekt im Thema Hausautomation. Da dieses Projekt dann doch recht groß wurde, teile ich das ganze in mehrere Schritte auf. Jetzt beschreibe ich Anfang und Allgemeines. Dann beschreibe ich wie ich die Module gebaut habe und anschließend das Aufsetzen des Systems auf dem Raspberry Pi.

## Übersicht und Anzeige

Zunächst erstmal, wie das alles jetzt für den Benutzer aussieht.

<figure style="text-align: center">
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/rooms_overview.PNG">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/rooms_overview_small.png">
	</a>
	<figcaption>
		Übersicht meiner Webapplikation mit Messwerten.
		Links Desktop-, Rechts Smartphoneansicht.
		Hier sehe ich aktuelle Temperatur, Feuchtigkeit, ob ein Fenster offen oder geschlossen ist und der Batteriezustand meiner Module.
	</figcaption>
</figure>

Im oberen Bild sieht man die Anzeige für aktuelle Daten. Das linke Teilbild zeigt einen Grundriss meiner Wohnung. Bisher sind drei Zimmer mit jeweils einem Modul ausgestattet. Hier kann ich direkt aktuelle Feuchtigkeit, Temperatur, Batteriestand und den Status der Fenster sehen. Grünes Fenster bedeutet es ist geschlossen, rotes Fenster wäre offen. 
Im rechten Teilbild sieht man die Darstellung für Smartphones. Da ich hier nicht so viel Anzeigefläche hab, müssen die Informationen natürlich ein wenig kompakter angezeigt werden.
Wenn ich mir den Verlauf von Temperatur und Feuchtigkeit des letzten Tages anzeigen lasse, schaut das wie folgt aus:

<figure style="text-align: center">
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/badezimmer_eintag.png">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/badezimmer_eintag_small.png">
	</a>
	<figcaption>
		Verlauf von Feuchtigkeit und Temperatur eines Tages. 
		Der Graph ist mit Highcharts-js dargestellt.
	</figcaption>
</figure>

Hier nutze ich Highcharts-js. Ein tolle Bibliothek für eine Weboberfläche zur Darstellung von Graphen. Es war mir wichtig dynamisch festlegen zu können, wie weit ich in die Vergangenheit schauen möchte. Ich kann also per Buttons und andere GUI[^GUI]-Elemente den zeitlichen Bereich (x-Achse) festlegen. Auf der rechten Seite, kann ich festlegen welche Elemente ich mir als Kurve anzeigen lassen will. Für jedes Element ist da ein kleines Bild.

[^GUI]: Graphical User Interface (Klick und Anzeigezeug)

## Grobe Planung

Ich hatte mir das alles so gedacht: **Ich baue mir Module mit denen ich Temperatur und Feuchtigkeit messen und an einen Raspberry Pi schicken kann.**

Ob ich dann später Temperatur regeln kann/will oder nicht, war mir erstmal nicht so wichtig. Dabei wollte ich nicht zu viel Geld ausgeben und mich trotzdem ein wenig mit "Technischer Informatik" beschäftigen. Der Plan war also zunächst zu verstehen was man alles dafür braucht und wie das dann alles funktionieren soll.

Nachdem ich mich also ein paar Stunden im Internet schlau gemacht hatte, hab ich mir ein paar Punkte dazu aufgestellt:

* Selber Module Bauen/Löten.
* Module sollen erweiterbar sein.
* Raspberry Pi als zentrales "Gehirn" des Ganzen.
* Das System soll erweiterbar sein (beliebig viele Module).
* Kosten so gering wie möglich (bin ja Student).
* Per Browser Zugriff und Anzeige auf aktuelle und gespeicherte Daten.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/raspberrypi/homeautomation/concept.png">
	<figcaption>
		Raspberry Pi als Basis und Empfänger.
		Die Sendermodule schicken nach und nach Informationen an die Basis.
	</figcaption>
</figure>

Nachdem man sich kurz mal nach Modulen und Hausautomation umgesehen hat, wird man schnell merken: Mist, das wird teuer!
Naja, nur wenn man die fertigen Module kauft. Wenn man wie ich erstmal nur Informationen zur Analyse sammeln möchte, kann man das sehr billig selbst bauen.
Gerade die Homepage mit den Projekten von <a href="http://nathan.chantrell.net/">Nathan Chantrell</a> haben mir da extrem geholfen. An dieser Stelle: Vielen Dank! Hier steht vieles darüber wie man selbst Funkmodule bauen kann und wie man damit Informationen versenden und empfangen kann.

Den Raspberry Pi hab ich aus folgenden Gründen gewählt:

* Es gibt eine riesige Community, die gern hilft.
* Es gibt schon unzählige Informationen und ähnliche Projekte.
* Er kostet nicht viel und verbraucht unglaublich wenig (4-5 Watt).

Ich hab mich ab da für Funk entschieden. Zum einen weil es dazu schon echt viel Informationen gibt und zum anderen, weil es sehr wenig Strom braucht Daten zu senden. Das schont Batterien und hält damit auch schön lang. Ich will ja nicht dauernd Batterien wechseln müssen...

So das schließt erst mal den ersten Schritt ab. Als nächstes werd' ich beschreiben, wie genau ich die Funkmodule gebaut habe.