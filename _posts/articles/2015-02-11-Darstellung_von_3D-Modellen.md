---
layout: article
title: "Darstellung von 3D-Modellen"
date: 2015-02-11
author: Christian
categories: articles
excerpt: "Aus was bestehen 3D-Modelle? Eine kurze Einführung in die Modellierung."
tags: [rendern]
toc: true
comments: true
image:
  feature: 
  teaser: Darstellung_von_3D_Modellen/Vorschau.jpg
---

Computergrafik verfolgt uns in jedem Bereich der mit Technik zu tun hat. In der Werbung, in Filmen, in Computerspielen, im Web, auf Smartphones und bald sicherlich auch als Hologramm. Dabei sind viele der dort sichtbaren Objekte von einem Designer am Rechner erstellt worden. Aber wie macht man sowas und wie sieht das aus?

Um 3D Modelle zu erstellen gibt es eine Vielzahl von Tools[^footnote]. Unterschiede gibt es in den Grundfunktionen fast gar nicht. Meist werde ich hier über 3DsMax schreiben, weil ich das als Student kostenlos bekomme und es eins der größten und bekanntesten Tools ist.
Trotzdem bleib ich dabei ganz allgemein, um mich nicht in Detailfunktionen zu verfangen.

[^footnote]: Hier die drei bekanntesten: 3DsMax/Maya von Autodesk, Cinema 4D von Maxon und Blender.

Als aller erstes schauen wir uns an woraus so ein Modell besteht.

<figure>
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/stone_and_displ_and_ao.jpg">
	<figcaption>Beispielmodell: Ein Turm.
	</figcaption>
</figure>


## **Die Grundstruktur**: Aus was bestehen 3D-Modelle?

Meist[^footnote] ist ein Modell aus lauter kleinen Dreiecken - **Polygonen** - aufgebaut. Die drei Ecken bzw. **Vertices** bilden mit ihren Kanten ein Polygon. Je mehr davon, desto detaillierter ist die Form. Das ist der Grundbaustein eines jeden Modells.
<!--{: .notice-info}-->

[^footnote]: Es gibt auch voxelbasiertes Rendern, worüber ich vielleicht ein andermal schreibe...

<figure style="text-align: center">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/polygon.gif">
	<figcaption>Ein Polygon.
	Hier dargestellt mit Vertices (rot) und Edges/Kanten (blau).
	</figcaption>
</figure>

Jedes Polygon hat zwei unterschiedliche Seiten. Eine Seite ist sichtbar - die andere nicht. Je nachdem wie die interne Reihenfolge der Vertices festgelegt ist (im Uhrzeigersinn oder gegen den Uhrzeigersinn) kann man das Polygon sehen oder nicht. Davon bekommt man selten etwas mit, deswegen kann man das im Zweifelsfall einfach umdrehen. Das Lot auf der Fläche des Polygons, die **Normale** der Fläche, deutet die Richtung an, in die das Polygon "zeigt". Bedeutet: Aus dieser Richtung kann man das Polygon sehen.

Sicher fragt man sich jetzt: "Wieso gibt es eine unsichtbare Seite?" Ganz einfache Grundregel: 

**Wieso etwas zeichnen das man nicht sehen kann?**
<!--{: .notice-info}-->

Polygone werden bei vielen Objekten nur für die Außenhülle berechnet, nicht das innere (sieht man ja eh nicht). Falls ein Polygon "falsch gepolt" wäre, also die Normale nach innen zeigen würde, fällt das sofort auf. An der Stelle wäre nämlich ein Loch und man kann dort durch das Objekt durchsehen. Natürlich ist das bei Glas oder anderen transparenten Gegenständen anders, im Regelfall aber spart man sich dadurch eine Menge Rechenleistung. Das leuchtet sicher noch mehr ein wenn man einen Schritt weiter geht.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/hemisphere.gif">
	<figcaption>Eine sehr simple halbe Kugel aus wenigen Polygonen. 
	</figcaption>
</figure>

Wenn man mehrere Polygone verbindet, entsteht ein Netz - auch **Mesh** genannt. Das stellt die Basis des Modells dar. Natürlich muss man nicht händisch all diese Polygone verbinden. Man kann relativ schnell aus Formen wie Würfeln, Kugeln, Ringe oder sonstigen Grundstrukturen einfache Formen erstellen.

Es gibt eine Vielzahl von Techniken und Möglichkeiten wie man von Grundformen zu Modellen kommt. Je nach Modell beginnt man auf eine andere Weise.
<!--{: .notice-info}-->


## Erstellen eines Meshes
<figure class="half" style="text-align: center">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/from_below.jpg">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/from_top.jpg">
	<figcaption>
		Je nach Distanz, Blickwinkel und Verwendungszweck variiert der nötige Detailgrad stark
	</figcaption>
</figure>


Bevor man ein Modell erstellt, sollte man sich immer im klaren sein wie detailliert es sein muss. Bin ich Befehlshaber mittelalterlicher Truppen in einem Strategiespiel oder befreie ich als Ritter die gefangene Prinzessin hoch oben im Turm nachdem ich mich durch Horden von Gegnern gemetzelt hab? Ja nachdem wie weit entfernt der Betrachter das Modell sieht, können Details ausgelassen und Polygone gespart werden. Je weniger Polygone und Effekte gezeichnet werden müssen, desto flüssiger läuft die Anwendung.

Leitspruch: **So wenig Polygone wie möglich, so viele wie nötig.**
<!--{: .notice-info}-->

Es reichen vielleicht sogar schon sehr grobe Strukturen. In diesem Fall ist das Fenster nur ein kleines Loch im Turm mit einem Steinbogen drum herum. Durch den Schatten und die Perspektive fällt es dann auch gar nicht auf, dass der Turm gar kein Innenleben hat. 

## Die grobe Form

Um einen Turm wie oben zu erstellen habe ich mit einem **Spline** begonnen und durch die **Lathe**-Funktion (Drehverfahren) einen Rotationskörper daraus erstellt. Das klingt jetzt erst einmal kryptisch, wird aber sicher durch eine kleine Erkärung und der Animation deutlich.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/spline_lathe.gif">
	<figcaption>
		Ein Rotationskörper aus einem Spline und der Lathe Funktion (Drehverfahren)
	</figcaption>
</figure>

Ein Spline ist ein Konstrukt aus Linien, Kurven und Ankerpunkten. Damit kann man grobe Umrisse und Formen zweidimensional vorzeichnen. Es reicht dabei nur die eine Hälfte der Form damit zu zeichnen. Die Lathe-Funktion erstellt dann ein Mesh durch Rotation um eine beliebige Achse im Raum. Dabei kann man Detailgrad, Richtung und Rotationswinkel angeben. Bei unserem Turm sind somit 36 Seiten bei vollen 360° entstanden. Für den ersten Schritt ist das völlig ausreichend.

## Verfeinerung

Sobald die grobe Form festliegt geht es an die Details. Es gibt unzählige Techniken und Methoden um aus der groben Form ein detailliertes Modell zu erstellen. Da können gut und gerne ein paar Wochen ins Land gehen. Es gibt Ausbildungsberufe und sogar ganze Studiengänge über dieses Thema. Am einfachsten ist es aber das nach und nach in Projekten oder Übungen zu lernen.

**Aber: Je mehr Erfahrung desto schneller versteht man welche Schraube man wann drehen muss.**

Hier in dem Turm-Beispiel zeig ich ein paar hilfreiche Tricks:

### Die Zinnen

Noch fehlen die Zinnen und das Fenster des Turms. Mit der **Extrude**-Funktion lassen sich Polygone "herausziehen" oder "hereinschieben". Eine sehr praktische Möglichkeit um mehr Details zu erzeugen. 

<figure style="text-align: center">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/extrude.gif">
	<figcaption>
		Durch die Extrude-Funktion kann man Polygone "herausziehen". Der Turm bekommt somit seine Zinnen.
	</figcaption>
</figure>

An der Oberseite des Turms wurden ein paar der Polygone "herausgezogen". Es wurden dabei zusätzliche Polygone erzeugt. Die stellen unsere Zinnen dar.

### Das Fenster

Das Modellieren eines Fensters wird schon ein wenig kniffliger. Man könnte jetzt mit händischer Kleinstarbeit Polygone schneiden und Vertices herumschieben (ziemlich umständlich), Flächen per Extrude hereinschieben und anpassen und und und... Ein wenig schneller geht es, wenn man das Fenster "herausstanzt". Dazu baut man sich einfach eine Art Stempel in Form eines Fensters.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/boolean_B.png">
	<figcaption>
		Stempel für das "Ausstechen" eines Fensters in den Turm.
	</figcaption>
</figure>

Nun brauchen wir nur noch über eine **boolsche** Funktion das Fenster aus dem Turm stechen. Mit einer boolschen Funktion (ähnlich der mathematischen Mengenlehre) kann man entweder die Kombination, die Schnittmenge oder die Subtraktion zweier Meshes erzeugen lassen. In unserem Fall hier wollen wir den Fensterstempel vom Turm subtrahieren.

<figure class="third">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/boolean_union.png">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/boolean_intersection.png">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/boolean_subtraction(A-B).png">
	<figcaption>Links: Kombination <br/>Mitte: Schnittmenge <br/>Rechts: Subtraktion (A-B)</figcaption>
</figure>

Gerade bei komplexeren Objekten spart man sich einen Haufen Arbeit. Wirklich sehr praktisch!

Damit wäre die Grundform unseres Turms fertig!

<figure class="third">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/boolean_subtraction(A-B).png">
	<figcaption>Fertige Form des Turms</figcaption>
</figure>
<!---
## **Texturen**: Die Wandfarbe der Modelle?

## Wie "tapeziere" ich mein Modell mit meinen Texturen?

## Ins richtige Licht rücken

### Body text
-->