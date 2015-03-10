---
layout: home
permalink: /
image:
  feature: Laptops.jpg
---

<div class="tiles">

<div class="tiles">
{% for post in site.posts %}
	{% if any(c.isalpha() for c in post.categories) %}
		{% include post-grid.html %}
	{% endif %}
{% endfor %}
</div><!-- /.tiles -->

</div><!-- /.tiles -->