---
layout: article
title: "Bilder komprimieren"
date: 2015-02-25
modified: 2015-03-25
author: Christian
categories: komprimierung
share: true
excerpt: "Was ist Komprimierung? Wie mache ich das mit Bildern?"
tags: [komprimieren, bilder]
toc: true
comments: true
image:
  feature: 
  teaser:  Komprimierung/Bilder_komprimieren/teaser.jpg
---

Vor 3 Jahren hat man sich noch über einen geschenkten USB-Stick mit 1 GB gefreut. Geht man heute auf eine Computermesse, überlegt man schon bei 2 GB, ob es das überhaupt Wert ist, dafür 5 Minuten in einer Schlange zu stehen. Zeitgleich wird das Internet immer schneller. Die Zugänge werden, soweit es geht, mit Glasfaserkabeln ausgestattet, und die Preise sinken stetig.

**Muss man noch auf Speicherplatz achten? Können wir nicht langsam auf Komprimierung verzichten und hohe Qualität beibehalten?**

Rechnen wir doch mal kurz durch:

## Rechenbeispiel

<figure style="text-align: center">
	<img src="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon.png" />
	<figcaption>
		Ein chinesischer Drache. 640x380 Pixel mit 256 Farben pro Kanal (Rot, Grün, Blau).
	</figcaption>
</figure>

Hier habe ich ein kleines Bild eines Drachen[^drache]. Das Bild ist genau 640 Pixel breit und 380 Pixel hoch. Insgesamt also 243200 Pixel. Eine sehr überschaubare Größe. Jeder Pixel des Bildes wird durch einen Farbwert beschrieben.

[^drache]: Das Modell des Drachen ist aus dem <a href="http://graphics.stanford.edu/data/3Dscanrep/">Stanford Repository</a> und wurde mit 3Ds Max gerendert. An dieser Stelle: Vielen Dank an das Stanford Computer Graphics Laboratory für die Bereitstellung!

Ein solcher Farbwert besteht hier aus einer Kombination von **R**ot, **G**rün und **B**lau (RGB). Diese Farben werden auch als Kanäle bezeichnet. Jeder Kanal kann jeweils 256 (8 Bit bzw. 1 Byte) Abstufungen haben. Ein Farbwert wird also durch drei Zahlen zwischen 0 und 255 dargestellt. Die Farbe Weiß wäre dementsprechend R:255, G:255, B:255, wobei Schwarz durch R:0, G:0, B:0 beschrieben wird.

## Kleiner Exkurs: Bits und Bytes

Wenn man Bits nicht nur aus dem Heimwerkerbereich kennt, kann man diesen Teil überspringen. Für den Rest hier ein kleiner Exkurs was Bits genau sind und wie man mit ihnen Zahlen darstellt.

Ein Bit kann mehrere Bedeutungen haben - "Aus" und "An", 0 und 1, "zu" und "offen", "ja" und "nein", etc. Was bei allen jedoch gleich ist: **Ein Bit beschreibt einen von zwei möglichen Zuständen**. Interpretiert man bei einem Hebel "oben" als 1 und "unten" als 0, so erhält man eine Binärzahl. 

<figure style="text-align: center">
	<img src="{{ site.url }}/images/Komprimierung/lever_10_example.png" />
	<figcaption>
		Zwei Hebel mit jeweils zwei möglichen Zuständen. Entweder oben oder unten. Bei zwei Hebeln hat man insgesamt 4 verschiedene Kombinationen:<br/>
		"unten" + "unten",<br/>
		"unten" + "oben",<br/>
		"oben" + "unten" und<br/>
		"oben" + "oben".
	</figcaption>
</figure>

Bei einer Binärzahl darf man nur die Ziffer 0 und die Ziffer 1 verwenden. So im alltäglichem Gebrauch verwenden wir das Dezimalsystem. Im Dezimalsystem sind pro Stelle die Ziffern 0-9 verwendbar. Hier zur Übersicht eine kleine Tabelle:

| Dezimal | Binär   |
|--------:|:--------|
|    0    |   0     |
|    1    |   1     |
|    2    |   10    |
|    3    |   11    |
|    4    |   100   |
|    5    |   101   |
|    6    |   110   |
|    7    |   111   |
|    8    |   1000  |
|    9    |   1001  |
|    10   |   1010  |

Bis zur Zahl **1** gibt es keinerlei Probleme. Ab der Zahl **2** jedoch, brauchen wir bei der Binärzahl eine weitere Stelle. Es sind ja nur die Ziffern 0 und 1 verwendbar. Ab der Dezimalzahl **4** und **8** brauchen wir jeweils eine weitere Stelle. Hier ist sicher nochmal gut zu sehen, dass bei einer Dezimalzahl 10 verschiedene Zeichen pro Stelle und bei einer Binärzahl immer nur 2 verschiedene Zeichen pro Stelle verwendet werden können. Man muss also bei Binärzahlen auch viel mehr Stellen nehmen, als in Dezimalzahlen, um die gleiche Zahl darzustellen.

Legt man vorher die Anzahl der Stellen fest, wird damit auch die maximal mögliche Zahl festgelegt, die man darstellen kann. Sprich: Wenn ich vorgebe, dass man nur **3** Stellen im Binärsystem verwenden kann, dann ist die höchste darzustellende Zahl die **7** (Binär: 111). Die kleinste Zahl, die man darstellen kann ist dabei immer die 0. Mit 3 Bit lassen sich somit die 8 verschiedenen Zahlen 0,1,2,3,4,5,6 und 7 darstellen. **Mit einem Byte sind 8 Bits, also 8 Stellen in einem Binärsystem, gemeint**. Die höchste Zahl, die man mit **8** Bits darstellen kann, ist die **255** (Binär: 11111111). Mit 8 Bits lassen sich also 256 verschiedene Zahlen darstellen (Nicht die **0** vergessen!).

Hier ein Beispiel, wie mit 8 Hebeln, die Zahl 175 dargestellt werden kann.
<figure style="text-align: center">
	<img src="{{ site.url }}/images/Komprimierung/lever_10101111_example.png" />
	<figcaption>
		Hier 8 Hebel, die die Zahl 175 darstellen. Binär: 10101111.
	</figcaption>
</figure>

## Weiter im Rechenbeispiel

**Pro Pixel müssen bei einem Farbbild also 3 Byte (24 Bit Farbtiefe) gespeichert werden**.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon_tooth.png" />
	<figcaption>
		Zoom auf einen Pixel am Zahn des Drachen. Der Farbwert beträgt dort R:148, G:133, B:0.
	</figcaption>
</figure>

Ein Farbwert wird beim RGB-Farbraum durch eine <a href="http://de.wikipedia.org/wiki/Additive_Farbmischung">additive Farbmischung</a> erreicht. Das kann man sich ungefähr so vorstellen: Man nimmt sich drei Farblampen (Rot, Grün und Blau) und richtet dieses im Dunkeln gegen eine weiße Wand. Stellt man nun entsprechend die Intensität der drei Lampen ein, kann man so jeden beliebigen Farbton des RGB-Farbraums erzeugen.

Das genaue Gegenteil wäre das Malen auf einem weißen Blatt Papier. Dort zieht man mit seinem Stift aus der weißen Farbe (R:255, G:255, B:255) bestimmte Farbwerte ab (<a href="http://de.wikipedia.org/wiki/Subtraktive_Farbmischung">substraktive Farbmischung</a>).

So kommen wir also auf 256 x 256 x 256 (also 3 Byte) Farbkombinationen pro Pixel. Sprich ca. 1,68 Millionen verschiedene Farbwerte.
Unkomprimiert erreichen wir bei 243200 Pixeln (640 x 380) genau 729600 Byte (=712,5 kByte). Alles noch im grünen Bereich?!

## Auflösungen, Megapixel und *-HD

Aktuelle Kameras unter 100€ schaffen locker 16 bis 20 Megapixel. Das bedeutet, dass die Kameras Bilder mit einer Auflösung von 4992 x 3328 Pixel und mehr erzeugen können. Wie sieht das im Vergleich zu gängigen Auflösungen im Standardgebrauch aus?

Dazu eine kleine Tabelle:

| MegaPixel | Auflösung	(Breite x Höhe) 	| Seitenverhältnis 	| Dateigröße [^dateigroesse] |
|----------:|:------------------------------|:-----------------:|---------------------------:|
|  0,3 MP   | 640  x 380					| 4:3 				|  0,70 MB					 |
|  0,8 MP   | 1024 x 768   					| 4:3   			|  2,25 MB					 |
|  0,9 MP   | 1280 x 720 (HDTV, 720p)		| 4:3				|  2,64 MB					 |
|  2,0 MP   | 1600 x 1200					| 4:3				|  5,49 MB					 |
|  2,1 MP   | 1920 x 1080 (Full HD, 1080p)	| 16:9				|  6,11 MB					 |
|  3,3 MP   | 2080 × 1560					| 4:3				|  9,28 MB					 |
|  8,3 MP   | 3840 × 2160 (UHD)				| 16:9				| 23,73 MB					 |
|  9,4 MP   | 4096 × 2304 (4K)				| 16:9 				| 27,00 MB					 |
| 12,0 MP   | 4048 × 3040					| 4:3				| 35,21 MB					 |
| 16,7 MP   | 4992 × 3328					| 3:2				| 47,53 MB					 |
| 22,0 MP	| 5344 × 4008					| 4:3				| 61,28 MB					 |

[^dateigroesse]: Dateigröße bei 24 Bit pro Pixel und ohne Komprimierung.

Näheres zu Megapixel siehe auf Wikipedia unter <a href="http://de.wikipedia.org/wiki/Bildaufl%C3%B6sungen_in_der_Digitalfotografie">Bildauflösung in der Digitalfotografie</a>.

Anhand der Tabelle erkennt man gut, dass bei doppelter Auflösung (z.B. ungefähr bei 2080 x 1560 <-> 4048 x 3040) die Megapixel (Pixelanzahl) und die Dateigröße um das 4-fache steigt.
Mit dem Thema, ob und wieso es so viel Megapixel gibt und ob das gut oder schlecht ist, werden wir uns hier aber nicht befassen. Jedoch kurz mal zum Nachdenken: 

**Welcher Monitor/Fernseher kann mir das darstellen? Möchte ich aus jedem Foto ein Plakat machen oder kann ich mir da nicht ein wenig Speicher sparen?**

Die derzeitige Standardauflösung 1920 x 1080 hat gerade mal 2 Megapixel. In naher Zukunft soll UHD bzw. 4K kommen und als Standard gelten. Selbst das kommt nicht einmal annähernd an 22 MP heran. Wozu also diese Unmengen an Megapixel? Das weiß nur der zahlungsfreudige Konsument...

**Tipp:** Wer nicht jedes einzelne Bild seiner Sammlung verkleinern will, kann das mit einem der vielen Tools aus dem Internet machen. Ein recht nettes Tool dazu wäre z.B. der <a href="https://imageresizer.codeplex.com/">Image Resizer</a> oder der <a href="http://www.faststone.org/FSResizerDetail.htm">FastStone Photo Resizer</a>. Probiert vorher ein wenig mit den Einstellungen herum! <br/> Achtung aber bei kostenlosen Online-Tools direkt im Browser! Eventuell gebt ihr dort eure Rechte ab. Unbedingt das Kleingedruckte lesen! Außerdem könnte das alles ganz schön lange dauern (muss ja erst hochgeladen werden).
{: .notice-info}

## Komprimierungsarten bei Bildern

Bei einer größeren Menge von Fotos (z.B. die alljährigen Urlaubsbilder), wird Komprimierung dann noch wichtiger. Die meisten Kameras komprimieren schon beim Auslösen, ohne das man etwas davon merkt. Automatisch kommen da JPG-Bilder raus und man muss sich um nichts mehr Gedanken machen... richtig? 

### Verlustfreie Komprimierung

Möchte man nicht auf Qualität jeglicher Art verzichten, gibt es immer noch die verlustfreie Komprimierung. Man spart sich also Speicherplatz, behält aber komplett die Qualität. Die Pixel selbst werden also nicht verändert. Bei Bildern nimmt man einfach das **Grafikformat PNG**. Das vorher genannte Bild des Drachen von **712,5 kB reduziert sich damit schon mal auf 191 kB**. Ein Drittel der vorherigen Größe und das ohne jeglichen Verlust!


##### Transparenz

Arbeitet man mit mehreren Schichten von Bildern, gibt es bei PNG optional einen Transparenzkanal.

<figure class="forth" style="text-align: center">
	<img src="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/transparent_example2.png" />
	<img src="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/transparent_example.png" />
	<figcaption>
		Zwei Bilder übereinander. Ein blaues Quadrat unter einem schwarzen Kreis mit Verlauf. <br/>
		Links PNG ohne Transparenzkanal (24 Bit), <br/>
		rechts PNG mit Transparenzkanal (32 Bit).
	</figcaption>
</figure>

Die Transparenz kann bei PNG mit weiteren 8 Bit pro Pixel angegeben werden. Dieser Kanal wird auch oft Alpha Kanal genannt. Diese 256 Abstufungen der Transparenz sind wichtig, um weiche Übergänge beschreiben zu können. Zuvor haben wir Bilder mit Pixeln betrachtet, die aus den Farben Rot, Blau und Grün bestehen. Mit dem Transparenzkanal wird ein Pixel mit 4 Kanälen (RGBA, **R**ot, **G**rün, **B**lau und **A**lpha) beschrieben und benötigt somit **32 Bit statt nur 24 Bit**. 

### Verlustbehaftete Komprimierung

Bei Fotos, die sowieso ein natürliches Rauschen haben, kann man auf perfekte Qualität verzichten und geringe Verluste akzeptieren. **Deswegen ist JPEG bei Fotos das bekannteste und meistgenutzte Grafikformat.** Praktisch ist zudem, dass man bei JPEG die Qualität in Prozent angeben kann. Bei einer Einstellung von 95%, also kaum Qualitätsverlust, ist der Unterschied mit bloßem Auge nicht zu erkennen. Ich seh da jedenfalls keinen Unterschied. Dabei reduziert sich jedoch die Dateigröße von 191 kB auf 36,2 kB (ca. 19% des PNG-Bilds).


<figure class="half" style="text-align: center">
	<a href="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon.png">
		<img src="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon.png" />
	</a>
	<a href="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon_95.jpg">
		<img src="{{ site.url }}/images/Komprimierung/Bilder_komprimieren/dragon_95.jpg" />
	</a>
	<figcaption>
		Links PNG mit 191 kB, rechts JPG 95% mit 36,2 kB.
	</figcaption>
</figure>

Reduziert man die Qualität weiter, fällt das erst mal gar nicht wirklich auf. Dazu ein paar Beispiele am Drachenbild.

#### Komprimierung des Drachenbildes

Das Bild hat weiterhin eine Auflösung von 640 x 380 Pixel und 24 Bit Farbtiefe.

| Komprimierung | Qualität 		| Dateigröße | Größe  |
|:--------------|:-------------:|:----------:|-------:|
| keine (BMP)	| original  	| 712,5 kB	 | 100,0% |
| PNG   		| verlustfrei   | 191,0 kB 	 | 26,8%  |
| JPEG  		| 95% 		  	| 63,2 kB    | 8,8%	  |
| JPEG   		| 75%   		| 17,3 kB    | 2,4%   |
| JPEG   		| 50%   		| 12,7 kB    | 1,8%	  |
| JPEG   		| 25%   		| 9,3 kB     | 1,3%   |

Erst bei einer Einstellung von 25% merkt erkennt man typische Anzeichen einer zu hohen Komprimierung. 
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

Wie man an Tabelle und Bilder sieht, ist Komprimierung nach wie vor ein sehr wichtiges Thema. Gerade bei einer großen Menge von Bildern, macht sich das am übrigen Speicherplatz deutlich. Das gilt natürlich auch für Filme und Videos, worüber ich aber in einem anderen Artikel schreiben werde.