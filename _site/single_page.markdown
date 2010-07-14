## [{{ page.title }}]({{ page.url }}) 
<div class="articleinfo">
pageed on {{ page.date | date_to_string }} by morygonzalez |
  {% for category in page.categories %}
    <a href="http://tech.portalshit.net/{{ category }}/">{{ category }}</a>
  {% endfor %}
</div>
{{ page.content }}
