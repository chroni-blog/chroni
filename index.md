---
layout: home
permalink: /
image:
  feature: Laptops.jpg
---

<div class="tiles">

<div class="tiles">
{% for post in site.posts %}
	{% unless post.category == "unpublished" %}
		{% include post-grid.html %}
	{% endunless %}
{% endfor %}
</div><!-- /.tiles -->

</div><!-- /.tiles -->