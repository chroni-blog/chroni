---
layout: article
title: "Gripsponse - Teil 1"
date: 2015-04-05
modified: 2015-04-12
author: Toni
categories: projekte
share: true
excerpt: "Gripsponse: Ein 3D Interaction Design von uns."
tags: [project, gripsponse, interaction]
toc: true
comments: true
image:
  feature:
  teaser: projekte/gripsponse.jpg
---

Was treiben Christian und ich eigentlich den ganzen Tag? Klar, wir sind Studenten und besuchen daher auch mal die ein oder andere Vorlesung, wenn es ganz böse kommt müssen wir sogar Prüfungen ablegen. Aber sonst? Nein, wir liegen nicht (nur) auf der faulen Haut und lassen die Sonne auf unsere blassen Bäuche scheinen. Wir sind sogar recht schaffenslustig. Ein Teil dieser Schaffenslust wird seit mittlerweile über einem Jahr vom Institut für Design und Informationssystem (IDIS) gestillt. Was das IDIS ist und was es macht, kann man auf der dazugehörigen [Homepage](http://idis.fhws.de){:target="_blank"} einfach mal nachlesen. 

In diesem Artikel möchte ich unser bis dato Hauptprojekt mit dem tollen Namen "Gripsponse" einmal etwas genauer vorstellen. 

##Was ist Gripsponse?

Ja, was ist Gripsponse nun? Nachdem Bilder mehr als tausend Worte sagen, hier gleich mal ein ganzes Video:

<iframe width="560" height="315" src="https://www.youtube.com/embed/4YlQ7xFUFmA" frameborder="0" allowfullscreen></iframe>

Der aufmerksame Leser/Zuschauer wird jetzt sicher denken: "DER 3D EFFEKT IST JA GEFÄLSCHT !!11Eins11elf". Ich kann euch beruhigen, er ist es. Das liegt hauptsächlich daran, dass unsere Kamera keine Shutter-Brille tragen wollte. 

Jetzt aber mal Spaß bei Seite, was habt ihr hier gerade gesehen? Gripsponse ist eine Software die eine gestenbasierte Steuerung von virtuellen Objekten ermöglicht. Es nutzt einen handelsüblichen 3D Fernseher mit [Shutter Technologie](http://www.hitec-handel.de/hitec-08/Online-Plus/pdf_pics/Samsung_Infografik3_ActiveShutterSystem_mitFliesstext.jpg){:target="_blank"} und einen Tiefensensor zur Gestenerkennung. Neben dem stereoskopischen Erlebnis werden sowohl zweidimensionale Anzeigen, als auch die Virtual Reality-Brille [Oculus Rift](https://www.youtube.com/watch?v=hZ8Xj_I3aNU){:target="_blank"} unterstützt. Die Interaktion mit dem virtuellen Objekt ist stark an die Realität angelehnt und somit sehr intuitiv zu nutzen.

##Aller Anfang ist leicht
Im Grunde haben wir uns zu Beginn von Gripsponse gefragt: Wie sieht die moderne Mensch-Computer-Interaktion aus - und was kommt nach Maus und Tastatur? Angefixt von zwei Professoren unsere Hochschule sowie Filmen wie "[Minority Report](https://www.youtube.com/watch?v=yzilZ33mk44){:target="_blank"}" und "[Iron Man](https://www.youtube.com/watch?v=_VFFLVyOEuc){:target="_blank"}" haben wir einfach mal angefangen der Frage auf den Grund zu gehen. 

Nachdem Christian im Rahmen seiner [Bachelorarbeit](http://petry-christian.de/volume_rendering/){:target="_blank"} sich intensiv mit der 3D Spiele-Engine Unity auseinandergesetzt hatte und ich mich im [Gegenzug](https://www.researchgate.net/profile/Toni_Fetzer/publications){:target="_blank"} mit der [Kinect von Microsoft](https://www.youtube.com/watch?v=oOCMr0D7BqY){:target="_blank"}, waren die Mittel zum Zweck recht schnell gefunden. Nur was machen damit? Am Anfang wollten wir vor allem zweierlei: Bewegung und Hologramme zum Anfassen! 

##Der erste Prototyp
Ich kümmerte mich also um eine ordentliche Anbindung der Kinect an [Unity3D](https://unity3d.com/){:target="_blank"} sowie der Übertragung der Position der Hände in die virtuelle Umgebung. Christian hatte sich währenddessen mit der Interaktion von virtuellen Objekten (im Video war es bspw. ein Motor) beschäftigt.[^1] Beides war recht schnell umgesetzt, woraus der erste kleine Prototyp (vgl. Bild #1) entstanden ist. Die Aufgabe für den Benutzer bestand lediglich darin, die Formen in die dafür vorgesehenen Löcher zu befördern. Um das ganze etwas schwieriger zu gestalten, hat sich die Fläche mit den Löchern horizontal im Raum gedreht. 

<figure>
	<a href="{{ site.url }}/images/projects/Gripsponse_1/prototyp_1.png">
		<img src="{{ site.url }}/images/projects/Gripsponse_1/prototyp_1.png" />
	</a>
	<figcaption>
		#1: So hat der erste Prototyp ausgesehen.
	</figcaption>
</figure>

Die Frage nach den Hologrammen hatte sich jedoch schwieriger erwiesen als zunächst erwartet. Es benötigte viel Feintuning und eine Menge Geduld um einen bestmöglichen [stereoskopischen Effekt](http://www.spektrum.de/lexikon/geowissenschaften/stereoskopischer-effekt/15673){:target="_blank"} zu erzeugen. Von echten Hologrammen zum Anfassen sind wir aber noch ein Stück entfernt (nicht nur wir, sondern auch die [Welt](http://obm.media.mit.edu/wp-content/uploads/sites/10/2012/09/barabasdissertation1-21-14a.pdf){:target="_blank"}). Hierfür müsste das dreidimensionale Objekt, welches aus dem Fernseher "herauskommt", direkt zwischen unseren Händen erscheinen. Das ist bisher jedoch nur mit [spezieller Hardware](https://www.youtube.com/watch?v=k8trP3V-tqE){:target="_blank"}, welche auch noch Ihre Schwächen hat, möglich. Grundsätzlich gilt jedoch, je mehr unser Auge von der virtuellen Umgebung sieht, desto besser ist der stereoskopische Effekt. Deshalb finden wir die VR-Brille Oculus Rift auch so spannend, denn hier versinken wir ganz und gar in der virtuellen Welt. Ob man dabei jedoch noch von Hologrammen sprechen kann, ist fraglich.

<figure>
	<a href="{{ site.url }}/images/projects/Gripsponse_1/interaction_1.png">
		<img src="{{ site.url }}/images/projects/Gripsponse_1/interaction_1.png" />
	</a>
	<figcaption>
		#2: Interaktion mit Objekten.
	</figcaption>
</figure>

Sinn des ersten Prototyps war es also eine Art Machbarkeitsstudie aufzustellen sowie erstes Feedback zum Interaktions Design zu erhalten. Funktioniert hat das System und die ca. 30 Tester hatten sichtlich Spaß damit. Im Hintergrund haben wir natürlich fleißig Daten gesammelt sowie die Nutzer einzeln zum System befragt. Das Ergebnis war, sagen wir, suboptimal. Zum Bewegen von Objekten hatten wir uns für eine kollisionsbasierte Variante entschieden. D.h. durch "pressen" der virtuellen Hände (die kleinen Vierecke in Bild #2) an das Objekt, konnte dieses bewegt werden. Hiermit hatten viele Nutzer Probleme bzw. erforderte es eine Menge Konzentration. Außerdem hatte es sich herausgestellt, dass nur die Hälfte aller Teilnehmer einen wirklichen Mehrwert aus dem stereoskopischen Effekt gezogen haben. Alles in allem war das Feedback an dieser Stelle unglaublich wertvoll für uns. Die iterative Vorgehensweise hat sich also mehr als bezahlt gemacht. In der nächsten Iteration ging es also darum, an unseren Fehlern des ersten Prototyps zu lernen.

Fortsetzung folgt...

[^1]: Ich verzichte hier bewusst auf die technischen Details, da wir sonst ganz viele tollen noch geplante Chroni Artikel vorwegnehmen würden.

