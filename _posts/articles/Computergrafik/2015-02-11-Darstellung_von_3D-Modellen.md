---
layout: article
title: "Darstellung von 3D-Modellen"
date: 2015-02-11
author: Christian
categories: computergrafik
excerpt: "Aus was bestehen 3D-Modelle? Eine kurze Einführung in die Modellierung."
tags: [rendern]
toc: true
comments: true
image:
  feature: 
  teaser: Darstellung_von_3D_Modellen/Vorschau.jpg
---

Computergrafik verfolgt uns in jedem Bereich der mit Technik zu tun hat. In der Werbung, in Filmen, in Computerspielen, im Web, auf Smartphones und bald sicherlich auch als Hologramm. Dabei sind viele der dort sichtbaren Objekte von einem Designer am Rechner erstellt worden. Aber wie macht man so was und was steckt dahinter?

Um 3D Modelle zu erstellen gibt es eine Vielzahl von Tools[^tools]. Unterschiede gibt es in deren Grundfunktionen fast gar nicht. Meist werde ich hier über 3DsMax schreiben, weil ich das als Student kostenlos bekomme und es eins der größten und bekanntesten Tools ist.
Trotzdem bleib ich dabei ganz allgemein und bei der Basis, um mich nicht in Detailfunktionen zu verfangen.

[^tools]: Hier die drei bekanntesten: 3DsMax/Maya von Autodesk, Cinema 4D von Maxon und Blender.

Als erstes schauen wir uns an woraus so ein Modell besteht.

<figure>
	<a href="{{ site.url }}/images/Darstellung_von_3D_Modellen/stone_and_displ_and_ao.jpg">
		<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/stone_and_displ_and_ao.jpg" />
	</a>
	<figcaption>
		Beispielmodell: Ein Turm.
	</figcaption>
</figure>


## **Die Grundstruktur**: Aus was bestehen 3D-Modelle?

Meist[^polygonbasiert] ist ein Modell aus lauter kleinen Dreiecken - **Polygonen** - aufgebaut. Die drei Ecken bzw. **Vertices** bilden mit ihren Kanten ein Polygon. Je mehr davon, desto detaillierter ist die Form. Das ist der Grundbaustein eines jeden Modells.
<!--{: .notice-info}-->

[^polygonbasiert]: Es gibt auch voxelbasiertes Rendern, worüber ich vielleicht ein andermal schreibe...

<figure style="text-align: center">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/polygon.gif" />
	<figcaption>Ein Polygon.
	Hier dargestellt mit Vertices (rot) und Edges/Kanten (blau).
	</figcaption>
</figure>

Jedes Polygon hat zwei unterschiedliche Seiten. Eine Seite ist sichtbar - die andere nicht. Je nachdem wie die interne Reihenfolge der Vertices festgelegt ist (im Uhrzeigersinn oder gegen den Uhrzeigersinn) kann man das Polygon sehen oder eben nicht. Von dieser Reihenfolge bekommt man selten etwas mit, deswegen kann man das Polygon im Zweifelsfall in der Anwendung einfach umdrehen. 
Das Lot auf der Fläche des Polygons, die **Normale** der Fläche, deutet die Richtung an, in die das Polygon "zeigt". Bedeutet: Aus dieser Richtung kann man das Polygon sehen.

Sicher fragt man sich jetzt: "Wieso gibt es eine unsichtbare Seite?" Ganz einfache Grundregel: 

**Wieso etwas zeichnen das man nicht sehen kann?**
<!--{: .notice-info}-->

Polygone werden bei vielen Objekten nur für die Außenhülle erstellt, nicht für das Innere (sieht man ja eh nicht). Falls ein Polygon "falsch gepolt" wäre, also die Normale nach innen zeigen würde, fällt das sofort auf. An der Stelle wäre nämlich ein Loch und man könnte dort durch das Objekt durchsehen. Ungewollt sieht das sehr unschön und fehlerhaft aus.
Gerade bei aufwändigen Grafikeffekten wie Beleuchtung und Schatten bedeutet eine geringe Polygonanzahl weniger Rechenaufwand. Deshalb ist es wichtig keine Polygone zu erstellen, die man nicht sehen kann. Das leuchtet sicher noch mehr ein wenn man einen Schritt weiter geht.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/hemisphere.gif" />
	<figcaption>Eine sehr simple halbe Kugel aus wenigen Polygonen. 
	</figcaption>
</figure>

Wenn man mehrere Polygone verbindet, entsteht ein Netz - auch **Mesh** genannt. Das stellt die Basis des Modells dar. Natürlich muss man nicht händisch all diese Polygone verbinden. Man kann relativ schnell aus Formen wie Würfeln, Kugeln, Ringe oder sonstigen Grundstrukturen einfache Formen erstellen.

Es gibt eine Vielzahl von Techniken und Möglichkeiten wie man von Grundformen zu Modellen kommt. Je nach Modell beginnt man auf eine andere Weise.
<!--{: .notice-info}-->


## Erstellen eines Meshes
<figure class="half" style="text-align: center">
	<a href="{{ site.url }}/images/Darstellung_von_3D_Modellen/from_below.jpg">
		<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/from_below.jpg" />
	</a>
	<a href="{{ site.url }}/images/Darstellung_von_3D_Modellen/from_top.jpg">
		<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/from_top.jpg" />
	</a>
	<figcaption>
		Je nach Distanz, Blickwinkel und Verwendungszweck variiert der nötige Detailgrad stark
	</figcaption>
</figure>


Bevor man ein Modell erstellt, sollte man sich immer im klaren sein wie detailliert es sein muss. Bin ich Befehlshaber mittelalterlicher Truppen in einem Strategiespiel oder befreie ich als Ritter die gefangene Prinzessin hoch oben im Turm nachdem ich mich durch Horden von Gegnern gemetzelt hab? Ja nachdem wie weit entfernt der Betrachter das Modell sieht, können Details ausgelassen und Polygone gespart werden. Je weniger Polygone und Effekte gezeichnet werden müssen, desto flüssiger läuft die Anwendung.

Leitspruch: **So wenig Polygone wie möglich, so viele wie nötig.**
<!--{: .notice-info}-->

Es reichen vielleicht sogar schon sehr grobe Strukturen. In diesem Fall ist das Fenster nur ein kleines Loch im Turm mit einem Steinbogen drum herum. Durch den Schatten und die Perspektive fällt es dann auch gar nicht auf, dass der Turm gar kein Innenleben hat. 

## Die grobe Form

Gehen wir zum Handwerk über. In jeder mir bekannten Software die sich mit der Modellierung von Objekten befasst, gibt einen Haufen Grundfunktionen. Hier gehe ich auf ein paar der wichtigsten drauf ein.

Um einen Turm wie oben zu erstellen habe ich mit einem **Spline** begonnen und durch die **Lathe**-Funktion (Drehverfahren) einen Rotationskörper daraus erstellt. Das klingt jetzt erst einmal kryptisch, wird aber sicher durch eine kleine Erkärung und der Animation deutlich.

<figure class="forth" style="text-align: center">
	<!-- Animation für Spline -->
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/spline.gif">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/spline_lathe.gif">
	<figcaption>Links: Verkettete Linien und Kurven - ein Spline.
		<br/>
		Rechts: Ein Rotationskörper aus einem Spline und der Lathe Funktion (Drehverfahren). Es entstehen 36 Seiten mit einer vollen Umdrehung.
	</figcaption>
</figure>

Ein Spline ist ein Konstrukt aus Linien, Kurven und Ankerpunkten. Damit kann man grobe Umrisse und Formen zweidimensional vorzeichnen. Es reicht dabei nur die eine Hälfte der Form damit zu zeichnen. Die Lathe-Funktion erstellt dann ein Mesh durch Rotation um eine beliebige Achse im Raum. Dabei kann man Detailgrad, Richtung und Rotationswinkel angeben. Bei unserem Turm sind somit 36 Seiten bei vollen 360° entstanden. Für den ersten Schritt ist das völlig ausreichend.

## Verfeinerung

Sobald die grobe Form festliegt geht es an die Details. Es gibt unzählige Techniken und Methoden um aus der groben Form ein detailliertes Modell zu erstellen. Da können gut und gerne ein paar Stunden ins Land gehen um die richtige Methode zu finden. Es gibt Ausbildungsberufe und sogar ganze Studiengänge über das Thema Modellierung und 3D-Design. Am einfachsten ist es wie so oft das nach und nach in Projekten oder Übungen zu lernen und sich Tipps aus Foren oder Youtube-Videos zu holen.

**Je mehr Erfahrung desto schneller versteht man, wann man was am besten macht.**

Hier am Turm-Beispiel zeig ich ein paar hilfreiche Tricks:

##### Die Zinnen

Noch fehlen die Zinnen und das Fenster des Turms. Um diese zu erzeugen gibt es zwei nützliche Funktionen.

<figure class="half" style="text-align: center">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/extrude.gif">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/chamfer.gif">
	<figcaption>
		Links: Durch die Extrude-Funktion kann man Polygone "herausziehen". Der Turm bekommt somit seine Zinnen. <br/>
		Rechts: Mit Chamfer kann man Ecken gut abrunden.
	</figcaption>
</figure>

Mit der **Extrude**-Funktion lassen sich Polygone "herausziehen" oder "hineinschieben". Eine sehr praktische Möglichkeit um mehr Details zu erzeugen. 
Wenn man die Kanten noch ein wenig abrunden möchte, hilft einem die **Chamfer**-Funktion weiter. Damit werden an den Kanten weitere Polygone erzeugt. 

An der Oberseite des Turms werden ein paar der Polygone ausgewählt und "herausgezogen". Rundet man diese noch ein wenig ab, sind unsere Zinnen auch schon fertig. So einfach ist das!

##### Das Fenster

Das Modellieren eines Fensters wird schon ein wenig kniffliger. Man könnte jetzt mit händischer Kleinstarbeit Polygone schneiden und Vertices herumschieben (ziemlich umständlich), Flächen per Extrude hineinschieben und und und... Ein wenig schneller geht es, wenn man das Fenster "herausstanzt". Dazu baut man sich einfach eine Art Stempel in Form eines Fensters.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/boolean_B.png">
	<figcaption>
		Stempel für das "Ausstechen" eines Fensters in den Turm.
	</figcaption>
</figure>

Nun brauchen wir nur noch über eine **boolsche** Funktion das Fenster aus dem Turm stechen. Mit einer boolschen Funktion (ähnlich der mathematischen Mengenlehre) kann man sich entweder die Kombination, die Schnittmenge oder die Subtraktion zweier Meshes erzeugen lassen. In unserem Fall hier wollen wir den Fensterstempel vom Turm subtrahieren.

<figure class="third" style="text-align: center">
	<a href="{{ site.url }}/images/Darstellung_von_3D_Modellen/boolean_union.png">
		<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/boolean_union.png">
	</a>
	<a href="{{ site.url }}/images/Darstellung_von_3D_Modellen/boolean_intersection.png">
		<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/boolean_intersection.png">
	</a>
	<a href="{{ site.url }}/images/Darstellung_von_3D_Modellen/boolean_subtraction(A-B).png">
		<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/boolean_subtraction(A-B).png">
	</a>
	<figcaption>Boolsche Funktion mit Turm (Objekt A) und Fensterstempel (Objekt B) <br/> Links: Kombination <br/>Mitte: Schnittmenge <br/>Rechts: Subtraktion (A-B)</figcaption>
</figure>

Gerade bei komplexeren Objekten spart man sich einen Haufen Arbeit. Wirklich sehr praktisch!

Damit wäre die Grundform unseres Turms fertig!

<!---
## **Texturen**: Die Wandfarbe der Modelle?

## Wie "tapeziere" ich mein Modell mit meinen Texturen?

## Ins richtige Licht rücken

### Body text
-->