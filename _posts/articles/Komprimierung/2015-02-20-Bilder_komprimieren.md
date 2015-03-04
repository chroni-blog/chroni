---
layout: article
title: "Bilder komprimieren"
date: 2015-02-25
author: Christian
categories: articles
excerpt: "Wie komprimiert man am besten Bilder?"
tags: [video]
toc: true
comments: true
image:
  feature: 
  teaser:  Komprimierung/Bilder_komprimieren/teaser.jpg
---

Verfügbarer Speicher wird Jahr für Jahr immer mehr und immer billiger. Vor 3 Jahren hat man sich noch über einen geschenkten USB-Stick mit 1GB gefreut. Geht man heute auf eine Computermesse, überlegt man schon bei 2GB ob es das überhaupt Wert ist dafür 5 Minuten in einer Schlange zu stehen. Zeitgleich wird das Internet immer schneller. Die Zugänge werden soweit es geht mit Glasfaserkabeln ausgestattet und die Preise sinken stetig.

**"Ich will alles in Full-HD und gestochen scharf! Komprimierung macht mir die Qualität kaputt!"**

Rechnen wir doch kurz mal durch:

## Rechenbeispiel

<figure style="text-align: center">
	<img src="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon.png" />
	<figcaption>
		Ein chinesischer Drache. 640x380 Pixel mit 256 Farben pro Kanal (Rot, Grün, Blau).
	</figcaption>
</figure>

Hier habe ich ein kleines Bild eines Drachen[^drache]. Das Bild ist genau 640 Pixel breit und 380 Pixel hoch. Insgesamt also 243200 Pixel. Ist ja noch überschaubar. Jeder Farbwert aus einer Kombination von rot, blau und grün besteht (RGB). Jeder Kanal (also R G oder B) kann jeweils 256 ( 8 Bit bzw. 1 Byte ) Abstufungen haben. Damit kommen wir auf 256 * 256 * 256 ( also 3 Byte ) Farben. Sprich ca. 1,68 Millionen mögliche Farbwerte. 

[^drache]: Das Modell des Drachen ist aus dem <a href="http://graphics.stanford.edu/data/3Dscanrep/">Stanford Repository</a> und wurde mit 3Ds Max gerendert. An dieser Stelle: Vielen Dank an das Stanford Computer Graphics Laboratory für die Bereitstellung!

**Pro Pixel muss also 3 Byte bei einem Bild mit 24 Bit Farbtiefe gespeichert werden**.

Unkomprimiert kommen wir also bei 243200 Pixeln auf 729600 B = 712,5 kB. Alles noch im grünen Bereich?!

## Auflösungen und Megapixel

Aktuelle Kameras unter 100€ schaffen locker 16 bis 20 Megapixel. Das bedeutet, dass die Kameras Bilder mit einer Auflösung von 4992 × 3328 Pixel erzeugen kann.

Eine kleine Tabelle dazu:

| MegaPixel | Auflösung	(Breite x Höhe) 	| Seitenverhältnis 	| Dateigröße | Größenfaktor |
|:----------|:-----------------------------:|:-----------------:|:----------:|-------------:|
|  0,3 MP   | 640  x 380					| 4:3 				|  0,70 MB	 |  1,00   		|
|  0,8 MP   | 1024 x 768   					| 4:3   			|  2,25 MB 	 |  3,21	    |
|  0,9 MP   | 1280 x 720 (HDTV, 720p)		| 4:3				|  2,64 MB	 |  3,77		| 
|  2,0 MP   | 1600 x 1200					| 4:3				|  5,49 MB   |  7,08	    | 
|  2,1 MP   | 1920 x 1080 (Full HD, 1080p)	| 16:9				|  6,11 MB   |  8,73	    | 
|  3,3 MP   | 2080 × 1560					| 4:3				|  9,28 MB   | 13,26		|
|  8,3 MP   | 3840 × 2160 (UHD)				| 16:9				| 23,73 MB   | 33,90		|
|  9,4 MP   | 4096 × 2304 (4K)				| 16:9 				| 27,00 MB	 | 38,57		|
| 12,0 MP   | 4048 × 3040					| 4:3				| 35,21 MB   | 50,30	    |
| 16,7 MP   | 4992 × 3328					| 3:2				| 47,53 MB   | 67,90	    |
| 22,0 MP	| 5344 × 4008					| 4:3				| 61,28 MB	 | 87,54		|

Näheres zu Megapixel siehe unter <a href="http://de.wikipedia.org/wiki/Bildaufl%C3%B6sungen_in_der_Digitalfotografie">Bildauflösung in der Digitalfotografie</a>.

Anhand der Tabelle erkennt man gut, dass bei doppelter Auflösung (z.B. ungefähr bei 2080 x 1560 <-> 4048 x 3040) die Megapixel (Pixelanzahl) und die Dateigröße um das 4-fache steigt.
Mit dem Thema ob und wieso es so viel Megapixel gibt und ob das gut oder schlecht ist soll hier nicht das Thema sein. Jedoch kurz mal zum Nachdenken: 

** Welcher Monitor/Fernseher kann mir das darstellen? Möchte ich aus jedem Foto ein Plakat machen? **

Die derzeitige Standardauflösung 1920 x 1080 hat gerade mal 2 Megapixel. In Zukunft soll UHD bzw. 4K kommen und standardisiert werden. Selbst das kommt nicht einmal annähernd an 22 MP heran.

## Komprimierungsarten bei Bildern

### Verlustfreie Komprimierung

Möchte man nicht auf Qualität jeglicher Art verzichten, gibt es immer noch die verlustfreie Komprimierung. Man spart sich also Speicherplatz und behält aber komplett die Qualität. Bei Bildern nimmt man einfach das Grafikformat PNG. Das vorher genannte Bild des Drachen von 712,5 kB reduziert sich damit auf 191 kB. Ohne Verlust!

### Verlustbehaftete Komprimierung

Kann man auf perfekte Qualität verzichten (z.B. bei Fotos, da diese sowieso geringes Rauschen haben) ist JPEG die bekannteste Möglichkeit.
Praktisch ist, dass man bei JPG die Qualität in Prozent angeben kann. Bei einer Einstellung von 95%, also kaum Qualitätseinbußen, ist der Unterschied nicht erkennbar. Dabei reduziert sich jedoch die Dateigröße von 191 kB auf 36,2 kB ( ca. 19% von dem PNG-Bild ).

<figure class="half">
	<a href="{{ site.url }}/images/Videos_komprimieren/dragon.png">
		<img src="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon.png" />
	</a>
	<a href="{{ site.url }}/images/Videos_komprimieren/dragon_95.jpg">
		<img src="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon_95.jpg" />
	</a>
	<figcaption>
		Links PNG mit 191 kB, rechts JPG 95% mit 36,2 kB.
	</figcaption>
</figure>


Reduziert man die Qualität jedoch weiter, fällt das erst mal gar nicht wirklich auf.
Hierzu eine kleine Tabelle:

#### Komprimierung des Drachenbildes

| Komprimierung | Qualität 		| Dateigröße | Größe in % |
|:--------------|:-------------:|:----------:|-----------:|
| keine (BMP)	| original  	| 712,5 kB	 | 100,0      |
| PNG   		| verlustfrei   | 191,0 kB 	 | 26,8		  |
| JPEG  		| 95% 		  	| 63,2 kB    | 8,8		  |
| JPEG   		| 75%   		| 17,3 kB    | 2,4		  |
| JPEG   		| 50%   		| 12,7 kB    | 1,8		  |
| JPEG   		| 25%   		| 9,3 kB     | 1,3 		  |

Zum direkten Vergleich ein Ausschnitt und die ganzen JPEG Bilder mit 95%, 75%, 50% und 25% nebeneinander.
<figure class="fourth" style="text-align: center">
	<img src="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon_mouth_95.png" />
	<img src="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon_mouth_75.png" />
	<img src="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon_mouth_50.png" />
	<img src="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon_mouth_25.png" />
</figure>

<figure class="fourth" style="text-align: center">
	<a href="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon_95.jpg">
		<img src="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon_95.jpg" />
	</a>
	<a href="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon_75.jpg">
		<img src="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon_75.jpg" />
	</a>
	<a href="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon_50.jpg">
		<img src="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon_50.jpg" />
	</a>
	<a href="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon_25.jpg">
		<img src="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon_25.jpg" />
	</a>
</figure>
