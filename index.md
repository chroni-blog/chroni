---
layout: home
permalink: /
image:
  feature: Laptops.jpg
---

<div class="tiles">

<div class="tiles">
{% for post in site.posts %}
	{% assign cat = post.categories%}
	{% cat.replace(' ', '')%}
	{% cat.rstrip()%}
	{% if cat != '' or cat != nil or cat) != blank %}
		{% include post-grid.html %}
	{% endif %}
{% endfor %}
</div><!-- /.tiles -->

</div><!-- /.tiles -->