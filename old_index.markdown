---
layout: default
---

{% for post in site.posts %}
## [{{ post.title }}]({{ post.url }})
<div class="articleinfo">
Posted on {{ post.date | date_to_string }} by morygonzalez |
	{% for category in post.categories %}
		<a href="http://tech.portalshit.net/{{ category }}/">{{ category }}</a>
	{% endfor %}
</div>
{{ post.content }}
{% endfor %}
