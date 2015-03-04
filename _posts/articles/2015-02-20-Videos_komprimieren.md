---
layout: article
title: "Videos komprimieren"
date: 2015-02-25
author: Christian
categories: articles
excerpt: "Was ist das? Was bringt das? Qualität - Dateigröße?"
tags: [video]
comments: true
image:
  feature: 
  teaser:  Videos_komprimieren/teaser.jpg
---

Verfügbarer Speicher wird Jahr für Jahr immer mehr und immer billiger. Vor 3 Jahren hat man sich noch über einen geschenkten USB-Stick mit 1GB gefreut. Geht man heute auf eine Computermesse, überlegt man schon bei 2GB ob es das überhaupt Wert ist dafür 5 Minuten in einer Schlange zu stehen. Zeitgleich wird das Internet immer schneller. Die Zugänge werden soweit es geht mit Glasfaserkabeln ausgestattet und die Preise sinken stetig.

**"Ich will alles in Full-HD und gestochen scharf! Komprimierung macht mir die Qualität kaputt!"**

Rechnen wir doch kurz mal durch:

## Rechenbeispiel:

<figure style="text-align: center">
	<img src="{{ site.url }}/images/Videos_komprimieren/dragon.png" />
	<figcaption>
		Ein chinesischer Drache. 640x380 Pixel mit 256 Farben pro Kanal (Rot, Grün, Blau).
	</figcaption>
</figure>

Hier habe ich ein kleines Bild eines Drachen[^drache]. Das Bild ist genau 640 Pixel breit und 380 Pixel hoch. Insgesamt also 243200 Pixel. Ist ja noch überschaubar. Jeder Farbwert aus einer Kombination von rot, blau und grün besteht (RGB). Jeder Kanal (also R G oder B) kann jeweils 256 ( 8 Bit bzw. 1 Byte ) Abstufungen haben. Damit kommen wir auf 256 * 256 * 256 ( also 3 Byte ) Farben. Sprich ca. 1,68 Millionen mögliche Farbwerte. 

[^drache]: Das Modell des Drachen ist aus dem <a href="http://graphics.stanford.edu/data/3Dscanrep/">Stanford Repository</a> und wurde mit 3Ds Max gerendert. An dieser Stelle: Vielen Dank an das Stanford Computer Graphics Laboratory für die Bereitstellung!

**Pro Pixel muss also 3 Byte bei einem Bild mit 24 Bit Farbtiefe gespeichert werden**.

Unkomprimiert kommen wir also bei 243200 Pixeln auf 729600 B = 712,5 kB. Alles noch im grünen Bereich. Aber es geht weiter:

<video width="640" height="380" controls style="text-align: center">
	<source src="{{ site.url }}/videos/videos_komprimieren/dragon_640x480_compressed_RF18.mp4" type="video/mp4">
	Your browser does not support the video tag or mp4 files.
</video>

Nun betrachten wir eine Kamerafahrt um den Drachen herum. Diese ist 10 Sekunden lang und spielt 30 Bilder pro Sekunde (FPS[^fps]) ab. 300 Bilder also insgesamt. Damit kommen wir auf 208 MB für das Video. Ab jetzt sollte einem langsam klar werden, dass das bei einem kompletten Film so nicht weitergehen kann. 

**Ein Film mit einer Länge von 120 Minuten hätte dann ca. 146 GB**. 

Damit wäre die externe Festplatte ziemlich schnell voll... Mit einem Film einer Auflösung von 640x380.

[^fps]:Frames per second

## Komprimierungsarten bei Bildern

### Verlustfreie Komprimierung

Möchte man nicht auf Qualität jeglicher Art verzichten, gibt es immer noch die verlustfreie Komprimierung. Man spart sich also Speicherplatz und behält aber komplett die Qualität. Bei Bildern nimmt man einfach das Grafikformat PNG. Das vorher genannte Bild des Drachen von 712,5 kB reduziert sich damit auf 191 kB. Ohne Verlust!

### Verlustbehaftete Komprimierung

Kann man auch minimal auf Qualität verzichten (z.B. bei Fotos) ist JPEG die bekannteste Möglichkeit.
Praktisch ist, dass man bei JPG die Qualität in Prozent angeben kann. Bei einer Einstellung von 95%, also kaum Qualitätseinbußen, ist der Unterschied nicht erkennbar. Dabei reduziert sich jedoch die Dateigröße von 191 kB auf 36,2 kB ( ca. 19% von dem PNG-Bild ).

<figure class="half">
	<a href="{{ site.url }}/images/Videos_komprimieren/dragon.png">
		<img src="{{ site.url }}/images/Videos_komprimieren/dragon.png" />
	</a>
	<a href="{{ site.url }}/images/Videos_komprimieren/dragon_95.jpg">
		<img src="{{ site.url }}/images/Videos_komprimieren/dragon_95.jpg" />
	</a>
	<figcaption>
		Links PNG mit 191 kB, rechts JPG 95% mit 36,2 kB.
	</figcaption>
</figure>


Reduziert man die Qualität jedoch weiter, fällt das erst mal gar nicht wirklich auf.
Hierzu eine kleine Tabelle:

#### Komprimierung des Drachenbildes

| Komprimierung | Qualität 		| Dateigröße |
|:--------------|:-------------:|-----------:|
| PNG   		| verlustfrei   | 191 kB   	 |
| JPEG  		| 95% 		  	| 63,2 kB    |
| JPEG   		| 75%   		| 17,3 kB    |
| JPEG   		| 50%   		| 12,7 kB    |
| JPEG   		| 25%   		| 9,33 kB    |

Zum direkten Vergleich die JPEG Bilder mit 75%, 50% und 25% nebeneinander.

<figure class="third" style="text-align: center">
	<a href="{{ site.url }}/images/Videos_komprimieren/dragon_75.jpg">
		<img src="{{ site.url }}/images/Videos_komprimieren/dragon_75.jpg" />
	</a>
	<a href="{{ site.url }}/images/Videos_komprimieren/dragon_50.jpg">
		<img src="{{ site.url }}/images/Videos_komprimieren/dragon_50.jpg" />
	</a>
	<a href="{{ site.url }}/images/Videos_komprimieren/dragon_25.jpg">
		<img src="{{ site.url }}/images/Videos_komprimieren/dragon_25.jpg" />
	</a>
	<figcaption>
		Von links nach rechts:
		JPEG 75%, JPEG 50%, JPEG 25%
	</figcaption>
</figure>


## Komprimierung bei Videos
...