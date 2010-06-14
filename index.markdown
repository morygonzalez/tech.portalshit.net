---
layout: default
---

{% for post in site.posts %}
## [{{ post.title }}]({{ post.url }})
<div class="articleinfo">
Posted on {{ post.date | date_to_string }} by morygonzalez
</div>
{{ post.content }}
{% endfor %}