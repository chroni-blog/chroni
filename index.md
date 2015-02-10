---
layout: home
permalink: /
image:
  feature: laptops.jpg
---

<div class="tiles">

<div class="tiles">
{% for post in site.categories.articles %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->

</div><!-- /.tiles -->