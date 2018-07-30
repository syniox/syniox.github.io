---
layout: default
---

*人可以卑微如尘土，但不可扭曲如蠕虫。*

{% for category in site.categories %}
<h2>{{ category | first }}</h2>
<ul class="arc-list">
    {% for post in category.last %}
      <li>{{ post.date | date_to_string }}　<a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
</ul>
{% endfor %}