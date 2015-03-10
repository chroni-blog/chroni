---
layout: home
permalink: /
image:
  feature: Laptops.jpg
---

<div class="tiles">

<div class="tiles">
{% for post in site.posts %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->

</div><!-- /.tiles -->