---
layout: home
permalink: /
image:
  feature: Laptops.jpg
---

<div class="tiles">

<div class="tiles">
{% for post in site.posts %}
	{% if post.categories contains "unpublished" or post.categories contains "examples" %}
	{% else if%}
		{% include post-grid.html %}
	{% endif%}
{% endfor %}
</div><!-- /.tiles -->

</div><!-- /.tiles -->