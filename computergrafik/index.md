---
layout: archive
title: "Computergrafik"
date: 2014-05-30T11:39:03-04:00
modified:
excerpt: "Hier steht was über Computergrafik oder so."
tags: []
image:
  feature: book.jpg
  teaser:
---

<div class="tiles">
{% for post in site.categories.computergrafik %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->