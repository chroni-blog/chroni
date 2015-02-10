---
layout: home
permalink: /
image:
  feature: wood-texture-1600x800.jpg
---

<div class="tiles">

<div class="tiles">
{% for post in site.categories %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->

</div><!-- /.tiles -->