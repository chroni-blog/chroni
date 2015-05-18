---
layout: article
title: "Gripsponse - Teil 2"
date: 2015-04-18
modified: 2015-04-26
author: Toni
categories: projekte
share: true
excerpt: "Doppelt gegriffen hält besser!"
tags: [project, gripsponse, interaction]
toc: false
comments: true
image:
  feature:
  teaser: projekte/gripsponse.jpg
---

Im dieser Serie habe ich etwas über die Intentionen hinter dem Projekt "Gripsponse" gesprochen. Außerdem wurde der ersten Prototyp sowie dessen Feedback Runde erläutert. Teil 2 setzt also genau in dieser Stelle an...

##Der zweite Prototyp
Nach Analyse der Datensätze und Fragebögen der ersten Testphase wurde uns eines klar: Die Wirkung der Stereoskopie wird unglaublich stark vom gewählten Interaktions Design beeinflusst. Deshalb lag unser Augenmerk auf einer Optimierung dessen. 

Es musste also ein Ersatz für die kollisionsbasierte Manipulation von Objektion her. Die neue Lösung sollte vor allem flexibel und robust sein. Flexibel im Sinne der unterschiedlichen Nutzergruppen und Robust in Hinblick auf schlechte Erkennung der Hände. Zum Beispiel direkte Sonneneinstrahlung auf den Tiefensensor kann zu einer Ungenauigkeit von bis zu 10 cm führen. Die virtuellen Hände des Nutzers springen dann wie wild im Bild umher, nicht cool! 

Um die Robustheit zu steigern hilft das sog. Smoothing. Das hat aber nichts mit Smoothies zu tun, sondern beschreibt viel mehr eine Art von Glättungsmechanismus. Diese bügeln extreme Bewegungssprünge aus und ermöglichen somit eine "smoothe" Interaktion. Beeinflusst der Algorithmus jedoch zu stark, hat man das Gefühl als wären die virtuellen Hände besoffen. Hier mussten wir also wieder einiges an Geduld für die optimale Parameter aufbringen. 

Unsere Lösung soll für jeden möglichst einfach sein und schnell erlernbar. Deshalb haben wir uns gegen aufwendige Gesten, wie Sie bspw. mit der Leap Motion möglich sind, entschieden. Es wird lediglich eine Geste von uns eingeführt: Das ballen beider Fäuste zum Greifen eines Objektes. Der volle Funktionsumfang kann aus der Grafik #1 entnommen werden. Erstaunlich wie viel man mit nur einer Geste machen kann, oder? Hierbei sei für die Rotation noch angemerkt, dass wir nicht in der Lage sind, die Neigung der Handgelenke herauszufinden und somit eine solche Rotation über "umgreifen" der Hände simuliert werden muss.

<figure>
	<a href="{{ site.url }}/images/projekte/Gripsponse_2/manipulation.png">
		<img src="{{ site.url }}/images/projekte/Gripsponse_2/manipulation.png" />
	</a>
	<figcaption>
		#1: Darstellung wie virtuelle Objekte manipuliert werden.
	</figcaption>
</figure>

Neben der reinen Manipulation von Objekten haben wir noch die Explosion, also das Aufsplitten eines Modells in seine Einzelteile, sowie das Snapping eingeführt. Beim Snapping wird eine sog. Boolesche Operation ausgeführt. Bei dieser wird überprüft ob sich ein vorher gelöstes Objekt komplett in seiner ursprünglichen Position befindet oder nicht. Bewegt man also ein Objekt in die Nähe seiner Ursprungsposition, so wird es automatisch an diese Stelle befördert und wie wir sagen "gesnappt". Das ist sehr praktisch, wenn ein Nutzer aus Übungszwecken bspw. den Motor in unserem Video auseinander und wieder zusammensetzen möchte, "rasten" die Einzelteile an die richtige Position wieder ein. Das Ganze manuell und ohne Snapping durchzuführen wäre nahezu ein Ding der Unmöglichkeit. 

<figure>
	<a href="{{ site.url }}/images/projekte/Gripsponse_2/vr-environment.jpg">
		<img src="{{ site.url }}/images/projekte/Gripsponse_2/vr-environment.jpg" />
	</a>
	<figcaption>
		#2: So hat der zweite Prototyp ausgesehen.
	</figcaption>
</figure>

Auch unser ursprüngliches Szenario des ersten Prototypen haben wir überarbeitet und sind zu dem Entschluss gekommen, das ein wenig Landschaft nicht schaden könnten. Da neben Erwachsenen aber auch Kinder Ihren Spaß haben sollten, haben wir uns für eine sehr spielerische Variante entschieden. Bild #2 zeigt die äußere Erscheinung des zweiten Prototyps. Wie das ganze funktioniert kann man sich ja leicht denken: Vor dem aktuellen Spieler können sechs unterschiedliche Formen erscheinen, jede dieser Form hat eine passende Lücke im Würfel. Ziel des Spiels ist es, die Teile möglichst schnell in die dafür vorgesehenen Löcher zu stecken. 

Hiermit möchte ich den etwas kürzen zweiten Teil beenden. Was die nächste Testphase zeigt, welche Auswirkungen das auf Christian und mich hatte und was das Land Slowenien damit zu tun hat, folgt im dritten Teil der Serie "Gripsponse". 

