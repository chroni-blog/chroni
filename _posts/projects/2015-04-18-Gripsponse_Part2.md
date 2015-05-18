---
layout: article
title: "Project: Gripsponse - Teil 2"
date: 2015-04-18
modified: 2015-04-18
author: Toni
categories: unpublished
share: true
excerpt: "Gripsponse: Ein 3D Interaction Design von uns."
tags: [project, gripsponse, interaction]
toc: true
comments: true
image:
  feature: 
  teaser:  Komprimierung/Bilder_komprimieren/teaser.jpg
---


[Hier geht es zu Teil 2]({% post_url /projects/2015-04-18-Gripsponse_Part2 %})


##Der zweite Prototyp
Nach Analyse der Datensätze und Fragebögen der ersten Testphase wurde uns eines klar: Die Wirkung der Stereoskopie wird unglaublich stark vom gewählten Interaktions Design beeinflusst. Deshalb lag unser Augenmerk für den Zweiten auf einer Optimierung dessen. 

Es musste also ein Ersatz für die kollisionsbasierte Manipulation von Objektion her. Die neue Lösung sollte vor allem flexibel und robust sein. Flexibel im Sinne der unterschiedlichen Nutzergruppen und Robust in Hinblick auf schlechte Erkennung der Hände. Zum Beispiel direkte Sonneneinstrahlung auf den Tiefensensor kann zu einer Ungenauigkeit von bis zu 10 cm führen. Die virtuellen Hände des Nutzers springen dann wie wild im Bild umher, nicht cool! 

Um die Robustheit zu steigern hilft das sog. Smoothing. Das hat aber nichts mit Smoothies zu tun, sondern beschreibt viel mehr eine Art von Glättungsalgorithmus. Diese bügeln extreme Bewegungssprünge aus und ermöglichen somit eine "smoothe" Interaktion. Beeinflusst der Algorithmus jedoch zu stark, hat man das Gefühl als wären die virtuellen Hände besoffen. Hier mussten wir also wieder einiges an Geduld für die optimale Parameter aufbringen. 

Unsere Lösung soll für jeden möglichst einfach sein und schnell erlernbar. Deshalb haben wir uns gegen aufwendige Gesten, wie Sie bspw. mit der Leap Motion möglich sind, entschieden. Es wird lediglich eine Geste von uns eingeführt: Das ballen beider Fäuste zum Greifen eines Objektes. Der volle Funktionsumfang kann aus unserem Poster (Bild #3) bzw. dem Video nun entnommen werden. 

Neben der reinen Manipulation von Objekten haben wir noch die Explosion, also das Aufsplitten eines Modells in seine Einzelteile, sowie das Snapping eingeführt. Beim Snapping wird eine sog. Boolesche Operation ausgeführt. Bei dieser wird überprüft ob sich ein vorher gelöstes Objekt komplett in seiner ursprünglichen Position befindet oder nicht. Bewegt man also ein Objekt in die Nähe seiner Ursprungsposition, so wird es automatisch an diese Stelle befördert und wie wir sagen "gesnappt". Das ist sehr praktisch, wenn ein Nutzer aus Übungszwecken bspw. den Motor in unserem Video auseinander und wieder zusammensetzen möchte, "rasten" die Einzelteile an die richtige Position wieder ein. Das Ganze manuell und ohne Snapping durchzuführen wäre nahezu ein Ding der Unmöglichkeit. 

Auch unser ursprüngliches Szenario aus Bild #1 haben wir überarbeitet und sind zu dem Entschluss gekommen, das ein wenig "Außenrum" nicht schaden könnten. Da neben Erwachsenen aber auch Kinder Ihren Spaß haben sollten, haben wir uns für eine sehr spielerische Variante entschieden. Bild #5 zeigt die äußere Erscheinung des zweiten Prototyps. Wie das ganze funktioniert kann man sich ja leicht denken: Vor dem aktuellen Spieler können sechs unterschiedliche Formen erscheinen, jede dieser Form hat eine passende Lücke im Würfel. Ziel des Spiels ist es, die Teile möglichst schnell in die dafür vorgesehenen Löcher zu stecken. 
