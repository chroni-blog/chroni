---
layout: article
title: "Projekt: Gripsponse - Teil 1"
date: 2015-04-01
modified: 2015-04-01
author: Toni
categories: unpublished
share: true
excerpt: "3D Interaction Design. Made by us."
tags: [rendern]
toc: true
comments: true
image:
  feature: 
  teaser: computergrafik/Darstellung_von_3D_Modellen/Vorschau.jpg
---

Polygone werden bei vielen Objekten nur für die Außenhülle erstellt, nicht für das Innere (sieht man ja eh nicht). Falls ein Polygon "falsch gepolt" wäre, also die Normale nach innen zeigen würde, fällt das sofort auf. An der Stelle wäre nämlich ein Loch und man könnte dort durch das Objekt durchsehen. Ungewollt sieht das sehr unschön und fehlerhaft aus.
Gerade bei aufwändigen Grafikeffekten wie Beleuchtung und Schatten bedeutet eine geringe Polygonanzahl weniger Rechenaufwand. Deshalb ist es wichtig keine Polygone zu erstellen, die man nicht sehen kann. Das leuchtet sicher noch mehr ein wenn man einen Schritt weiter geht.