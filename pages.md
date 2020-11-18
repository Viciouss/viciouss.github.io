---
layout: default
title: Pages
---

# Pages

<ul>
{% for page in site.static_pages %}
    <li><a href="{{ page.url }}">{{ page.title }}</a></li>
{% endfor %}
</ul>
