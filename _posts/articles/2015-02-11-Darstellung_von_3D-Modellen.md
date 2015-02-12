---
layout: article
title: "Darstellung von 3D-Modellen"
date: 2015-02-11
author: Christian
categories: articles
excerpt: "Wie werden 3D-Modelle auf einem Display dargestellt? Eine kurze Einführung in die Computergrafik."
tags: [rendern]
toc: true
comments: true
image:
  feature: Darstellung_von_3D_Modellen/stone_and_displ_and_ao.jpg
  teaser: Darstellung_von_3D_Modellen/Vorschau.jpg
---

Computergrafik verfolgt uns in jedem Bereich der mit Technik zu tun hat. In der Werbung, in Filmen, in Computerspielen, im Web, auf Smartphones und bald sicherlich auch als Hologramm. Doch wieso sieht das Auto in der Werbung so real aus? Wieso sehen Autos in Computerspielen nicht genauso gut aus? Wo liegen die Unterschiede?

Als aller erstes schauen wir uns an was woraus so ein Modell besteht.

## **Die Grundstruktur**: Aus was bestehen 3D-Modelle?

Meist[^footnote] besteht ein Modell aus lauter kleinen Dreiecken, **Polygonen**. Jedes Polygon hat zwei unterschiedliche Seiten. Eine Seite ist sichtbar - die andere nicht. Das Lot auf der Fläche des Polygons, die **Normale**, zeigt uns die Richtung aus der das Polygon sichtbar ist.

[^footnote]: Es gibt auch voxelbasiertes Rendern, worüber ich vielleicht ein andermal schreibe...

<figure>
	<img src="{{ site.url }}/images/Darstellung_von_3D_Modellen/polygon.gif">
	<figcaption>Ein Polygon.
	Hier dargestellt mit Vertices (rot) und Edges/Kanten (hellblau). (</figcaption>
</figure>

Wenn man mehrere Polygone verbindet, entsteht ein Netz - auch **Mesh** genannt. Das stellt die Basis eines Modells dar. Natürlich muss man nicht händisch all diese Polygone verbinden. Man kann relativ schnell aus Formen wie Würfeln, Kugeln, Ringe oder sonstigen Grundstrukturen erstellen.

## **Texturen**: Die Wandfarbe der Modelle?

## Wie "tapeziere" ich mein Modell mit meinen Texturen?

## Ins richtige Licht rücken

### Body text
