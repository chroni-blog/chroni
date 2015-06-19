---
layout: archive
title: "Projekte"
date: 2015-04-07
modified: 2015-05-18
excerpt: "Aktuelle und vergangene Projekte."
tags: []
image:
  feature:
  teaser:
---

<div class="tiles">
{% for post in site.categories.projekte %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->
