---
layout: default
---

<center>"自己选择的路，跪着也要走完。"</center>

**Disabled at the moment.**
temp: qzkszj.coding.me

{% for category in site.categories %}
<h2>{{ category | first }}</h2>
<ul class="arc-list">
    {% for post in category.last %}
      <li>{{ post.date | date_to_string }}　<a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
</ul>
{% endfor %}
