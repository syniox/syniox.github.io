---
layout: default
---

*人可以卑微如尘土，但不可扭曲如蠕虫。*

{% for post in site.posts %}

{{ post.date | date_to_string }} <a href="{{ post.url }}">{{ post.title }}</a>  

{% endfor %}