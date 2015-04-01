---
layout: archive
title: "Projekte"
date: 2014-05-30T11:39:03-04:00
modified:
excerpt: "Hier steht was über unsere Projekte."
tags: []
image:
  feature: book.jpg
  teaser:
---

<div class="tiles">
{% for post in site.categories.projects %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->