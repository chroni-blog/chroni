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

Was treiben Christian und ich eigentlich den ganzen Tag? Klar, wir sind Studenten und besuchen daher auch mal die ein oder andere Vorlesung, wenn es ganz böse kommt müssen wir sogar Prüfungen ablegen. Aber sonst? Nein, wir liegen nicht (nur) auf der faulen Haut und lassen die Sonne auf unsere blassen Bäuche scheinen. Wir sind sogar recht schaffenslustig. Ein Teil dieser Schaffenslust wird seit mittlerweile über einem Jahr vom Institut für Design und Informationssystem (IDIS) gestillt. Was das IDIS ist und was es macht, kann man auf der dazughörigen Homepage einfach mal nachlesen. 

In diesem Artikel möchte ich unser bis dato Hauptprojekt mit dem tollen Namen "Gripsponse" einmal etwas genauer vorstellen. 

##Was ist Gripsponse? [^1]

Ja, was ist Gripsponse nun? Nachdem Bilder mehr als tausend Worte sagen, hier gleich mal ein ganzes Video:

<iframe width="560" height="315" src="https://www.youtube.com/embed/4YlQ7xFUFmA" frameborder="0" allowfullscreen></iframe>

Der aufmerksame Leser/Zuschauer wird jetzt sicher denken: "DER 3D EFFEKT IST JA GEFÄLSCHT !!11Eins11elf". Ich kann euch beruhigen, er ist es. Das liegt hauptsächlich daran, das unsere Kamera keine Shutter-Brille tragen wollte. 

Jetzt aber mal Spaß bei Seite, was habt ihr hier gerade gesehen? Gripsponse ist eine Software die eine gestenbasierte Steuerung von virtuellen Objekten ermöglicht. Es nutzt einen handelsüblichen 3D Fernseher mit einer sogenannten Shutter Technologie und einen Tiefensensor zur Gestenerkennung. Neben dem stereoskopischen Erlebnis werden sowohl zweidimensionale Anzeigen, als auch die Virtual Reality-Brille Oculus Rift unterstützt. Die Interaktion mit dem virtuellen Objekt ist stark an die Realität angelehnt und somit sehr intuitiv zu nutzen.

####Aller Anfang ist leicht
Im Grunde haben wir uns zu Beginn von Gripsponse gefragt: Wie sieht die moderne Mensch-Computer-Interaktion aus - und was kommt nach Maus und Tastatur? Angefixt von zwei Professoren unsere Hochschule sowie Filmen wie "Minority Report" und "Iron Man" haben wir einfach mal angefangen der Frage auf den Grund zu gehen. 

Nachdem Christian im Rahmen seiner Bachelorarbeit sich intensiv mit der 3D Spiele-Engine Unity auseinandergesetzt hatte und ich mich im Gegenzug mit der Kinect von Microsoft, waren die Mittel zum Zweck recht schnell gefunden. Nur was machen damit? Am Anfang wollten wir vor allem zweierlei: Bewegung und Hologramme zum anfassen! 

##Der erste Prototyp
Ich kümmerte mich also um eine ordentliche Anbindung der Kinect an Unity sowie der Übertragung der Position der Hände in die virtuelle Umgebung. Christian hatte sich währenddessen mit der Interaktion von virtuellen Objekten (im Video war es bspwl. ein Motor) beschäftigt. Beides war recht schnell umgesetzt, worraus der erste kleine Prototyp (vgl. Bild ) enstanden ist. Die Aufgabe für den Benutzer bestand lediglich darin, die Formen in die dafür vorgesehenen Löcher zu befördern. Um das ganze etwas schwieriger zu gestalten, hat sich die Fläche mit den Löchern horizontal im Raum gedreht. 

Die Frage nach den Hologrammen hatte sich jedoch schwieriger erwiesen als zunächst erwartet. Es benötigte viel Feintuning und eine Menge Geduld um einen bestmöglichen stereoskopischen Effekt zu erzeugen. Von echten Hologrammen zum Anfassen sind wir aber leider noch weit entfernt (nicht nur wir, sondern auch die Welt). Hierfür müsste das dreidimensionalle Objekt, welches aus dem Fernseher "herrauskommt", direkt zwischen unseren Händen erscheinen. Das ist bisher jedoch nur mit spezieller Hardware, welche auch noch Ihre Schwächen hat, möglich. Grundsätzlich gilt jedoch, je mehr unser Auge von der virtuellen Umgebung sieht, desto besser ist der stereoskopische Effekt. Deshalb finden wir die VR-Brille Oculus Rift auch so spannend, denn hier versinken wir ganz und gar in der virtuellen Welt. Ob man dabei jedoch noch von Hologrammen sprechen kann, ist fraglich.

Sinn des ersten Prototyps war es also eine Art Machbarkeitsstudie aufzustellen sowie erstes Feedback zum Interaktions Design zu erhalten. Funkioniert hat das System und die ca. 30 Tester hatten sichtlich Spaß damit. Im Hintergrund haben wir natürlich fleißig Daten gesammelt sowie die Nutzer einzeln zum System befragt. Das Ergebnis war, sagen wir, supoptimal. Zum Bewegen von Objekten hatten wir uns eine kollisionsbasierte Variante entschieden. D.h. durch "drücken" der virtuellen Hände (die kleinen Vierrecke in Bild .. ) an das Objekt, konnte dieses bewegt werden. Hiermit hatten viele Nutzer Probleme bzw. erforderte es eine Menge Konzentration. Außerdem 



[^1]: Ich verzichte hier bewusst auf die technischen Details, da wir sonst ganz viele tollen noch geplante Chroni Artikel vorwegnehmen würden. 

