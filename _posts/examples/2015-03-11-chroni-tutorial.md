---
layout: article
title: "Chroni 1.0: Ein Tutorial"
date: 2015-03-11
modified: 
excerpt:
tags: []
image:
  feature:
  teaser:
  thumb:
toc: true
share: false
categories: examples
---

## Technische Basis des Blogs

Chroni basiert auf [Jekyll]. Jekyll ist wiederum ein auf [Liquid] und [Markdown] basierender Blog-Generator. Ein großer Vorteil von Jekyll ist die nicht benötigte Datenbank, es werden also nur statische Seiten erzeugt. Die Details hierzu können den einzelnen Dokumentationen entnommen werden, oder mit mir besprochen werden. Weiter unten folgt ein wenig mehr über Jekyll sowie dem eingesetzten [YAML Front Matter].

Als Markdown-Converter wird [Kramdown] eingesetzt, das zum einen eine höhere Funktionalität wie das Standard Markdown aufweist, sowie wirklich schönes Code-Highlightning sowie LaTeX Injections erlaubt. Für den Autor heißt das, Artikel werden in Kramdown geschrieben. Hierzu empfiehlt sich der Einsatz eines [Online-Editors]. Dieser kann ach relativ einfach lokal installiert werden (siehe [Github-Projekt]). Für einen schnelle und einfachen Einstieg in Kramdown sei die [Quick Reference] empfohlen. 

Chroni.de wird komplett auf Github gehostet. Für den Autor bedeutet das, er muss das Projekt zunächst via Git vom Github-Repository auschecken. Wer noch nie etwas mit Git zutun hatte, sollte sich auf jeden Fall die [Helps von Github] sowie die offizielle [Git Dokumentation] ansehen. Auch hier empfehle ich, mich oder Christian einfach mal zu kontaktieren, falls es Fragen gibt. 

[Jekyll]: http://jekyllrb.com/docs/home/ "Jekyll-Homepage"
[Liquid]: https://github.com/Shopify/liquid/wiki "Liquid auf Github"
[Markdown]: http://daringfireball.net/projects/markdown/ "Offiziele Markdown Webpräsenz"
[Kramdown]: http://kramdown.gettalong.org/index.html "Kramdown Webpräsenz"
[Online-Editors]: http://kramdown.herokuapp.com/ "Kramdwon Online-Editor"
[Github-Projekt]: https://github.com/unindented/online-kramdown-sinatra "Github Projekt des Online Editors"
[Quick Reference]: http://kramdown.gettalong.org/quickref.html "Kramdown Quick References"
[Helps von Github]: http://git-scm.com/documentation "Github Helppage"
[Git Dokumentation]: https://help.github.com/ "Offizielle Git Dokumentation"
[YAML Front Matter]: http://www.yaml.de/ "YAML Front Matter"

---

## Schreiben eines Artikels

Artikel werden logischerweise in `.md` Markdown-Files geschrieben. Damit es am Schluss kein totales Chaos gibt, werden benennen wir Artikel beginnend mit dem Datum, gefolgt vom Titel. Ein Beispiel wäre: `2015-03-11-new-post.md`. 

#### YAML Front Matter
Ein ganz besonders wichtiger Punkt ist das YAML Front Matter Framework oder auch inoffiziell Header des Artikels. Die einzelnen Variablen werden anhand folgendem Beispiel erklärt:

<pre>
<code>
layout: article
title: "Das ist der Titel des Artikels"
categories: auto
excerpt: "Hier möchte ich euch etwas übe Autos erzählen."
share: true
image:
  feature: branch-1600x800.jpg
  teaser: branch-400x250.jpg
  credit: Michael Rose
  creditlink: http://mademistakes.com
toc: true
modified: 2015-02-27
comments: true
</code>
</pre>

Die einzigen von YAML Front Matter geforderten Werte sind `title` und `layout`, der Rest ist optional. Bei `layout` handelt es sich um unter `/_layouts` gespeicherten HTML-Dateien, welche das strukturelle Aussehen eines Artikels beschreiben. Neue Layouts sollten nur nach Absprache mit Christian und mir erstellt werden. Das Bearbeiten bestehender Layouts ist NICHT vorgesehen, da hierbei das Aussehen aller Artikel verändert wird, welche dieses Layout einsetzen. Außerdem ist es durch Kramdown möglich, HTML Code innerhalb eines Artikels zu injecten, was diverses Costumizing des einzelnen Artikels zulässt. 

Auf chroni.de werden alle Artikel in Kategorien einsortiert. Jeder Artikel enthält zum aktuellen Zeitpunkt lediglich **eine** Kategorie. Um eine neue Kategorie zu erstellen muss nichts weiteres gemacht werden, als diese unter `categories:` einzutragen. Bei der Speicherung von Artikeln sind dennoch einige Dinge zu beachten. Weiter unten gehe ich etwas genauer darauf ein. 

`excerpt` beschreibt den Textabschnitt, der auf der Main unterhalb des Teaser-Bildes angezeigt wird. 

Falls die Option `share` auf `true` eingestellt ist, werden die Share-Buttons für Facebook und co eingeschaltet. Grundsätzlich befürworten wir das. 

Innerhalb des `image:` Blocks wird zum einen das `feature:` sowie das `teaser:` Bild angezeigt. Die Bilder werden im Verzeichnis `/images` abgelegt. Das Featurebild wird aktuell nur im Layout `media.html` an oberster Stelle des Artikels angezeigt. Das Teaserbild ist das kleine Vorschaubild innerhalb einer Artikelübersicht. 

Das Keyword `toc` steht für Table of Content, setzt man diese auf `true` wird in der rechten oberen Ecke des Textes ein Inhaltsverzeichnis angezeigt. Überschriften müssen in Markdown mit `##Überschrift` geschrieben werden, damit sie im Table of Content aufgenommen werden.  

Wann ein Artikel das letzte mal geändert wurde, kann mit Hilfe von `modified:` bestimmt werden. 

Die Kommentare werden über die externe Plattform [Disqus] realisiert. Grundsätzlich befürworten wir eine Kommentarfunktion und schalten Sie über `comments: true` ein. 


[Disqus]: https://disqus.com/ "Disques Webseite"

#### Speicherung von Artikeln
Artikel werden unter Jekyll als Post bezeichnet und immer im Verzeichnis `_posts` abgelegt. Wenn ein Post nun beispielsweise der Kategorie `auto` angehört, sollte dieser aus reinen Gründen der Übersichtlichkeit unter `_posts/auto` abgelegt werden. Ja, das bedeutet, das es eigentlich total egal ist, wo euer Artikel innerhalb von `_posts` liegt, Hauptsache die Kategorie unter `categories:` wurde richtig bezeichnet. Falls ihr gerade an einem Artikel sitzt, der noch nicht für die Augen der Öffentlichkeit bereit ist, gebt einfach im Header unter `categories:` die Kategorie `unpublished` an, dadurch erscheint euer Artikel noch nicht auf der Main, sondern lediglich unter `chroni.de/unpublished`. Falls ihr schlussendlich fertig seid, einfach `categories:` auf die gewünschte Kategorie abändern. 

Wie oben bereits erwähnt, nutzen wir Kramdown als Markdown Converter. Unter der Kategorie `examples` können einige Beispiele für den Einsatz von Kramdown angesehen werden. Diese können auch hier im Browser aufgerufen werden. 

[hier]: http://www.chroni.de/examples/ "Beispiele Kramdown"

#### Neue Seite für eine Kategorie erstellen
Falls man sich entschließen sollte, eine neue Kategorie anzulegen, muss eine sog. Übersichtsseite für alle Artikel aus dieser Rubrik entstehen. Hierfür wird innerhalb des Homeverzeichnisses des Repositorys `./` ein neuer Ordner mit dem Namen der Kategorie in Kleinbuchstaben erstellt werden. Beispielsweise `/auto`. Um die betroffenen Artikeln nun anzeigen zu können, kopieren wir die `index.md` Datei zum Beispiel aus der Kategorie `computergrafik` in unser Verzeichnis `/auto` und verändern die Codezeile `{% for post in site.categories.computergrafik %}` zu `{% for post in site.categories.auto %}`. Nun werden alle Artikel mit der Kategorie `auto` automatisch unter `chroni.de/auto` angezeigt. 

#### Kategorie zum Slider Menü hinzufügen
Gibt es nun min. 2 Artikel mit ein und derselben Kategorie, erstellen wir einen neuen Menüpunkt innerhalb des Sliders, also den kleinen schwarzen Button rechts oben. Hierfür wird das File `/_data/slidenavigation.yml` geöffnet und weiter Eintrag hinzugefügt. Am besten einfach einen alten Eintrag kopieren und lediglich die Werte anpassen. Das ganze ist relativ selbsterklärend. 

#### Autoren hinzufügen

#### Cheatsheet: Neuen Artikel schreiben
1. Artikel eindeutig benennen 
2. YAML Header schreiben
3. Kategorie zunächst als `unpublished`
4. Artikel fertig?
	1. Schreibe Artikel
5. Kategorie auswählen bzw. selbst bestimmen
6. Ist es eine neue Kategorie?
	1. In `_posts` neuen Ordner mit Namen der Kategorie erstellen
	2. Artikel in diesen Ordner speichern
	3. Erstellen einer neuen Seite für die Kategorie 
	4. Kategorie zum Slider Menü hinzufügen
7. Neuer Autor? 
	1. Autor hinzufügen 
