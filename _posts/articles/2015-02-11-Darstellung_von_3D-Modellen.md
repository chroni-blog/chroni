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

Meist[^footnote] ist ein Modell aus lauter kleinen Dreiecken - **Polygonen** - aufgebaut. Die drei Ecken bzw. **Vertices** bilden mit ihren Kanten ein Polygon. Je mehr davon desto detaillierter die Form. Das ist der Grundbaustein eines jeden Modells.
<!--{: .notice-info}-->

[^footnote]: Es gibt auch voxelbasiertes Rendern, worüber ich vielleicht ein andermal schreibe...

<figure style="text-align: center">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/polygon.gif">
	<figcaption>Ein Polygon.
	Hier dargestellt mit Vertices (rot) und Edges/Kanten (blau).
	</figcaption>
</figure>

Die Polygone haben zwei unterschiedliche Seiten. Eine Seite ist sichtbar - die andere nicht. Je nachdem wie die interne Reihenfolge der Vertices festgelegt ist (im Uhrzeigersinn oder gegen den Uhrzeigersinn) kann man das Polygon sehen oder nicht. Das Lot auf der Fläche des Polygons, die **Normale** der Fläche, zeigt dabei die Richtung, in die das Polygon "zeigt". Bedeutet: Aus dieser Richtung kann man das Polygon also sehen.

Sicher fragt man sich jetzt: "Wieso gibt es eine unsichtbare Seite?" Ganz einfache Grundregel: 

Wieso etwas zeichnen/berechnen was man nicht braucht?
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


Bevor man ein Modell erstellt sollte man sich immer im klaren sein wie detailliert es sein muss. Bin ich Befehlshaber mittelalterlicher Truppen in einem Strategiespiel oder befreie ich als Ritter die gefangene Prinzessin hoch oben im Turm nachdem ich mich durch Horden von Gegnern gemetzelt hab? Ja nachdem wie genau der Betrachter das Modell sehen kann, können Details ausgelassen und Polygone gespart werden. Denn gerade darauf kommt es an. 

So wenig Polygone wie möglich, so viele wie nötig. 
<!--{: .notice-info}-->

Es reichen vielleicht sogar schon sehr grobe Strukturen. In diesem Fall ist in das Fenster nur ein kleines Loch mit einem Steinbogen drum herum. Durch den Schatten und die Perspektive fällt das auch gar nicht auf.

<figure style="text-align: center">
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/spline_lathe.gif">
	<figcaption>
		Ein Rotationskörper aus einem Spline und der Lathe Funktion (Drehverfahren)
	</figcaption>
</figure>

Um einen Turm wie oben zu erstellen habe ich mit einem **Spline** begonnen und durch die **Lathe**-Funktion (Drehverfahren) einen Rotationskörper daraus erstellt. Ein Spline ist ein Konstrukt aus Linien, Kurven und Ankerpunkten. Damit kann man grobe Umrisse und Formen zweidimensional vorzeichnen. Die Lathe-Funktion erstellt dann ein Mesh durch Rotation um eine beliebige Achse im Raum.

Sobald die grobe Form festliegt geht es an die Details. Noch fehlen die Zinnen und das Fenster des Turms. Mit der **Extrude**-Funktion lassen sich Polygone "herausziehen" oder "hereinschieben". Eine sehr praktische Möglichkeit um mehr Details zu erzeugen. 

Das Fenster wird schon ein wenig kniffliger. Man könnte jetzt mit händischer Kleinstarbeit Polygone schneiden und Vertices herumschieben, Flächen per Extrude hereinschieben und anpassen und und und. Ein wenig schneller geht es, wenn man das Fenster "herausstanzt". Dazu baut man sich einfach eine Art Stempel in Form eines Fensters. In Kombination einer **Boolschen**-Funktion (ähnlich der mathematischen Mengenlehre) kann man entweder die Schnittmenge zweier Meshes, die Kombination oder die Subtraktion beider Modelle erzeugen lassen. In unserem Fall hier wollen wir den Fensterstempel vom vorherigen Mesh subtrahieren. Wirklich sehr praktisch!

Damit wäre die Grundform unseres Turms fertig!

<!---
## **Texturen**: Die Wandfarbe der Modelle?

## Wie "tapeziere" ich mein Modell mit meinen Texturen?

## Ins richtige Licht rücken

### Body text
-->