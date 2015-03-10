---
layout: home
permalink: /
image:
  feature: Laptops.jpg
---

<div class="tiles">

<div class="tiles">
{% for page in site.pages %}
	{% unless page.categories == "unpublished" or page.categories == ""%}
		{% include post-grid.html %}
	{% endunless %}
{% endfor %}
</div><!-- /.tiles -->

</div><!-- /.tiles -->