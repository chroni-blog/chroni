---
layout: article
title: "Homeautomation mit dem Raspberry Pi - Teil 1"
date: 2015-07-07
modified: 2015-07-07
author: Christian
categories: unpublished
share: true
excerpt: "Temperaturmessung zum Selbstbauen mit dem Raspberry Pi"
tags: [raspberrypi, homeautomation]
toc: true
comments: true
image:
  feature: 
  teaser: raspberrypi/mediencenter/mediencenter_teaser.png
---

Kaum hat man mal ein wenig mehr Erfahrung mit dem Raspberry Pi, kommt man auf allerlei Ideen. Es gibt automatische [Mediencenter](../Mediencenter){:target="_blank"}, Web- und Datenserver, [Spielekonsole](../Mediencenter_2){:target="_blank"}, Aquariensteuerungen, Sprenkleranlagen, uvm.
Hier beschreibe ich mal ein Projekt im Thema Hausautomation. Da dieses Projekt dann doch recht groß wurde, teile ich das ganze in mehrere Schritte auf. Jetzt erstmal beschreibe ich Anfang und Allgemeines. Dann beschreibe ich wie ich die Module gebaut habe und danach das Aufsetzen des Systems auf dem Raspberry Pi.

<figure style="text-align: center">
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/rooms_overview.PNG">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/rooms_overview_small.png">
	</a>
	<figcaption>
		Übersicht meiner Webapplikation mit Messwerten.
		Hier sehe ich aktuelle Temperatur, Feuchtigkeit, ob ein Fenster offen oder geschlossen ist und der Batteriezustand meiner Module.
	</figcaption>
</figure>

**Ich hatte mir das alles so gedacht: Ich baue mir Module mit denen ich Temperatur und Feuchtigkeit messen und an einen Raspberry Pi schicken kann.**

Ob ich dann später Temperatur regeln kann/will oder nicht, war mir erstmal nicht so wichtig. Dabei wollte ich nicht zu viel Geld ausgeben und trotzdem ein wenig mit Technischer Informatik mich beschäftigen. Der Plan war also erstmal zu verstehen was man alles dafür braucht und wie das dann alles funktionieren soll.

Nachdem ich also ein paar Stunden mich im Internet schlau gemacht hab, hab ich mir ein paar Punkte aufgestellt:

* Selber Module Bauen/Löten.
* Module sollen erweiterbar sein.
* Raspberry Pi als zentrales "Gehirn" des ganzen.
* Kosten so gering wie möglich (bin ja Student).
* Per Browser Zugriff und Anzeige auf aktuelle und gespeicherte Daten.

Im oberen Bild sieht man die Anzeige für aktuelle Daten. Wenn ich mir den Verlauf anzeigen lasse, schaut das wie folgt aus:
<figure style="text-align: center">
	<a href="{{ site.url }}/images/raspberrypi/homeautomation/badezimmer_eintag.PNG">
		<img src="{{ site.url }}/images/raspberrypi/homeautomation/badezimmer_eintag_small.png">
	</a>
	<figcaption>
		Verlauf von Feuchtigkeit und Temperatur eines Tages. Der Graph ist mit Highcharts.js dargestellt.
	</figcaption>
</figure>


Nachdem man sich kurz mal nach Modulen und Hausautomation umgesehen hat wird man schnell merken: **Mist, das wird teuer!**
Naja, nicht unbedingt. Wenn man wie ich erstmal nur Informationen zur Analyse sammeln möchte, kann man das sehr billig selbst bauen.
Gerade die Homepage mit den Projekten von <a href="http://nathan.chantrell.net/">Nathan Chantrell</a> haben mir extrem geholfen. An dieser Stelle: Vielen Dank! Hier steht vieles darüber wie man selbst Funkmodule bauen kann und wie man damit Informationen versenden und empfangen kann.

Den Raspberry Pi hab ich aus folgenden Gründen gewählt: 
* Es gibt eine riesige Community, die gern hilft.
* Es gibt schon unzählige Informationen und ähnliche Projekte.
* Er kostet nicht viel und verbraucht unglaublich wenig (4-5 Watt).

Ich hab mich ab da für Funk entschieden. Zum einen weil es dazu schon echt viel Informationen gibt und zum anderen, weil es sehr wenig Strom braucht. Das schont Batterien und hält damit dann auch schön lang. Will ja nicht dauernd Batterien wechseln...
