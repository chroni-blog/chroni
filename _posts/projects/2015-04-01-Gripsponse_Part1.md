---
layout: article
title: "Project: Gripsponse - Teil 1"
date: 2015-04-01
modified: 2015-04-01
author: Toni
categories: unpublished
share: true
excerpt: "Gripsponse: Ein 3D Interaction Design von uns."
tags: [komprimieren, bilder]
toc: true
comments: true
image:
  feature: 
  teaser:  Komprimierung/Bilder_komprimieren/teaser.jpg
---

Was treiben Christian und ich eigentlich den ganzen Tag? Klar, wir sind Studenten und besuchen daher auch mal die ein oder andere Vorlesung, wenn es ganz böse kommt müssen wir sogar Prüfungen ablegen. Aber sonst? Nein, wir liegen nicht (nur) auf der faulen Haut und lassen die Sonne auf unsere blassen Bäuche scheinen. Wir sind sogar recht schaffenslustig. Ein Teil dieser Schaffenslust wird seit mittlerweile über einem Jahr vom Institut für Design und Informationssystem (IDIS) gestillt. Was das IDIS ist und was es macht, kann man auf der dazugehörigen Homepage einfach mal nachlesen. 

In diesem Artikel möchte ich unser bis dato Hauptprojekt mit dem tollen Namen "Gripsponse" einmal etwas genauer vorstellen. 

##Was ist Gripsponse?

Ja, was ist Gripsponse nun? Nachdem Bilder mehr als tausend Worte sagen, hier gleich mal ein ganzes Video:

<iframe width="560" height="315" src="https://www.youtube.com/embed/4YlQ7xFUFmA" frameborder="0" allowfullscreen></iframe>

Der aufmerksame Leser/Zuschauer wird jetzt sicher denken: "DER 3D EFFEKT IST JA GEFÄLSCHT !!11Eins11elf". Ich kann euch beruhigen, er ist es. Das liegt hauptsächlich daran, das unsere Kamera keine Shutter-Brille tragen wollte. 

Jetzt aber mal Spaß bei Seite, was habt ihr hier gerade gesehen? Gripsponse ist eine Software die eine gestenbasierte Steuerung von virtuellen Objekten ermöglicht. Es nutzt einen handelsüblichen 3D Fernseher mit einer sogenannten Shutter Technologie und einen Tiefensensor zur Gestenerkennung. Neben dem stereoskopischen Erlebnis werden sowohl zweidimensionale Anzeigen, als auch die Virtual Reality-Brille Oculus Rift unterstützt. Die Interaktion mit dem virtuellen Objekt ist stark an die Realität angelehnt und somit sehr intuitiv zu nutzen.

####Aller Anfang ist leicht[^1]
Im Grunde haben wir uns zu Beginn von Gripsponse gefragt: Wie sieht die moderne Mensch-Computer-Interaktion aus - und was kommt nach Maus und Tastatur? Angefixt von zwei Professoren unsere Hochschule sowie Filmen wie "Minority Report" und "Iron Man" haben wir einfach mal angefangen der Frage auf den Grund zu gehen. 

Nachdem Christian im Rahmen seiner Bachelorarbeit sich intensiv mit der 3D Spiele-Engine Unity auseinandergesetzt hatte und ich mich im Gegenzug mit der Kinect von Microsoft, waren die Mittel zum Zweck recht schnell gefunden. Nur was machen damit? Am Anfang wollten wir vor allem zweierlei: Bewegung und Hologramme zum anfassen! 

##Der erste Prototyp
Ich kümmerte mich also um eine ordentliche Anbindung der Kinect an Unity sowie der Übertragung der Position der Hände in die virtuelle Umgebung. Christian hatte sich währenddessen mit der Interaktion von virtuellen Objekten (im Video war es bspw. ein Motor) beschäftigt. Beides war recht schnell umgesetzt, woraus der erste kleine Prototyp (vgl. Bild #1) entstanden ist. Die Aufgabe für den Benutzer bestand lediglich darin, die Formen in die dafür vorgesehenen Löcher zu befördern. Um das ganze etwas schwieriger zu gestalten, hat sich die Fläche mit den Löchern horizontal im Raum gedreht. 

<figure>
	<a href="{{ site.url }}/images/projects/Gripsponse_1/prototyp_1.png">
		<img src="{{ site.url }}/images/projects/Gripsponse_1/prototyp_1.png" />
	</a>
	<figcaption>
		#1: So hat der erste Prototyp ausgesehen.
	</figcaption>
</figure>

Die Frage nach den Hologrammen hatte sich jedoch schwieriger erwiesen als zunächst erwartet. Es benötigte viel Feintuning und eine Menge Geduld um einen bestmöglichen stereoskopischen Effekt zu erzeugen. Von echten Hologrammen zum Anfassen sind wir aber leider noch weit entfernt (nicht nur wir, sondern auch die Welt). Hierfür müsste das dreidimensionale Objekt, welches aus dem Fernseher "herauskommt", direkt zwischen unseren Händen erscheinen. Das ist bisher jedoch nur mit spezieller Hardware, welche auch noch Ihre Schwächen hat, möglich. Grundsätzlich gilt jedoch, je mehr unser Auge von der virtuellen Umgebung sieht, desto besser ist der stereoskopische Effekt. Deshalb finden wir die VR-Brille Oculus Rift auch so spannend, denn hier versinken wir ganz und gar in der virtuellen Welt. Ob man dabei jedoch noch von Hologrammen sprechen kann, ist fraglich.

<figure>
	<a href="{{ site.url }}/images/projects/Gripsponse_1/interaction_1.png">
		<img src="{{ site.url }}/images/projects/Gripsponse_1/interaction_1.png" />
	</a>
	<figcaption>
		#2: Interaktion mit Objekten.
	</figcaption>
</figure>

Sinn des ersten Prototyps war es also eine Art Machbarkeitsstudie aufzustellen sowie erstes Feedback zum Interaktions Design zu erhalten. Funktioniert hat das System und die ca. 30 Tester hatten sichtlich Spaß damit. Im Hintergrund haben wir natürlich fleißig Daten gesammelt sowie die Nutzer einzeln zum System befragt. Das Ergebnis war, sagen wir, suboptimal. Zum Bewegen von Objekten hatten wir uns für eine kollisionsbasierte Variante entschieden. D.h. durch "pressen" der virtuellen Hände (die kleinen Vierecke in Bild #2) an das Objekt, konnte dieses bewegt werden. Hiermit hatten viele Nutzer Probleme bzw. erforderte es eine Menge Konzentration. Außerdem hatte es sich herausgestellt, dass nur die Hälfte aller Teilnehmer einen wirklichen Mehrwert aus dem stereoskopischen Effekt gezogen haben. Alles in allem war das Feedback an dieser Stelle unglaublich wertvoll für uns. Die iterative Vorgehensweise hat sich also mehr als bezahlt gemacht. In der nächsten Iteration ging es also darum, an unseren Fehlern des ersten Prototyps zu lernen.

##Der zweite Prototyp
Nach Analyse der Datensätze und Fragebögen der ersten Testphase wurde uns eines klar: Die Wirkung der Stereoskopie wird unglaublich stark vom gewählten Interaktions Design beeinflusst. Deshalb lag unser Augenmerk für den Zweiten auf einer Optimierung dessen. 

Es musste also ein Ersatz für die kollisionsbasierte Manipulation von Objektion her. Die neue Lösung sollte vor allem flexibel und robust sein. Flexibel im Sinne der unterschiedlichen Nutzergruppen und Robust in Hinblick auf schlechte Erkennung der Hände. Zum Beispiel direkte Sonneneinstrahlung auf den Tiefensensor kann zu einer Ungenauigkeit von bis zu 10 cm führen. Die virtuellen Hände des Nutzers springen dann wie wild im Bild umher, nicht cool! 

Um die Robustheit zu steigern hilft das sog. Smoothing. Das hat aber nichts mit Smoothies zu tun, sondern beschreibt viel mehr eine Art von Glättungsalgorithmus. Diese bügeln extreme Bewegungssprünge aus und ermöglichen somit eine "smoothe" Interaktion. Beeinflusst der Algorithmus jedoch zu stark, hat man das Gefühl als wären die virtuellen Hände besoffen. Hier mussten wir also wieder einiges an Geduld für die optimale Parameter aufbringen. 

Unsere Lösung soll für jeden möglichst einfach sein und schnell erlernbar. Deshalb haben wir uns gegen aufwendige Gesten, wie Sie bspw. mit der Leap Motion möglich sind, entschieden. Es wird lediglich eine Geste von uns eingeführt: Das ballen beider Fäuste zum Greifen eines Objektes. Der volle Funktionsumfang kann aus unserem Poster (Bild #3) bzw. dem Video nun entnommen werden. 

Neben der reinen Manipulation von Objekten haben wir noch die Explosion, also das Aufsplitten eines Modells in seine Einzelteile, sowie das Snapping eingeführt. Beim Snapping wird eine sog. Boolesche Operation ausgeführt. Bei dieser wird überprüft ob sich ein vorher gelöstes Objekt komplett in seiner ursprünglichen Position befindet oder nicht. Bewegt man also ein Objekt in die Nähe seiner Ursprungsposition, so wird es automatisch an diese Stelle befördert und wie wir sagen "gesnappt". Das ist sehr praktisch, wenn ein Nutzer aus Übungszwecken bspw. den Motor in unserem Video auseinander und wieder zusammensetzen möchte, "rasten" die Einzelteile an die richtige Position wieder ein. Das Ganze manuell und ohne Snapping durchzuführen wäre nahezu ein Ding der Unmöglichkeit. 

Auch unser ursprüngliches Szenario aus Bild #1 haben wir überarbeitet und sind zu dem Entschluss gekommen, das ein wenig "Außenrum" nicht schaden könnten. Da neben Erwachsenen aber auch Kinder Ihren Spaß haben sollten, haben wir uns für eine sehr spielerische Variante entschieden. Bild #5 zeigt die äußere Erscheinung des zweiten Prototyps. Wie das ganze funktioniert kann man sich ja leicht denken: Vor dem aktuellen Spieler können sechs unterschiedliche Formen erscheinen, jede dieser Form hat eine passende Lücke im Würfel. Ziel des Spiels ist es, die Teile möglichst schnell in die dafür vorgesehenen Löcher zu stecken. 

##Forschungsfrage und eine Konferenz
Bereits nach der Feedback Runde des ersten Prototyps wurden einige Stimmen laut, unserem Projekt eine wissenschaftlichere Note zu geben und nicht nur grob nach einer neuen Art der Mensch-Computer-Interaktion zu fragen. Hierfür haben wir uns auf einen Faktor gestützt, der uns von herkömmlichen Lösungen unterschiedet: Dem stereoskopischen Effekt. Neben der Programmierarbeit ging es also zusätzlich noch darum folgende Forschungsfrage zu überprüfen: "".

Wie es in der Wissenschaft nun mal so üblich ist, langt es nicht eine Hypothese einfach so zu verifizieren/falsifizieren, es muss natürlich auch ein mehrseitiges wissenschaftliches Papier dazu geschrieben werden. Wo kämmen wir denn sonst hin, wenn man seine Ergebnisse einfach so mir nichts dir nichts im Internet veröffentlichen würde ;). [^2] 

Anstatt einer einfachen Feedback Runde, wurde nun eine Studie mit 50 Teilnehmern im Alter zwischen 6 und 60 Jahren durchgeführt. Hierfür wurden zwei Gruppen gebildet, die entweder mit der monoskopischen Anzeige (normales TV-Bild) oder der stereoskopischen Anzeige (3D-TV) begonnen haben. Nach einem kompletten Testdurchlauf wurden die Anzeigetechnik dann pro Gruppe gewechselt. Als Testumgebung kam unser Puzzle-Spiel des zweiten Prototypen zum Einsatz. Es wurden die Zeiten gemessen, die ein Proband zum Einsetzen der sechs Teile in den Würfel gebraucht hat sowie die subjektive Meinung über einen Fragebogen ermittelt. 




[^1]: Ich verzichte hier bewusst auf die technischen Details, da wir sonst ganz viele tollen noch geplante Chroni Artikel vorwegnehmen würden.
 
[^2]: Aber mal im Ernst, mir macht das Schreiben von wissenschaftlichen Arbeiten sogar richtig Spaß, sonst hätte ich wohl auch keinen Blog mit diesen Themen!


