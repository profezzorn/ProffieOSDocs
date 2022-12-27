---
title: Single-page documentation
---

{% assign dirs = site.pages | group_by: "dir" | sort: "name" %} 

{% for dir in dirs %}
{%if dir.name != "/" and dir.name != "/assets/css/" %}
*****
# {{ dir.name | remove_first: "/" | split: "/" | join: ", " | capitalize }}
*****
{% endif %}
  {% for p in dir.items %}
    {% if p.url != "/" and p.url != "/all_pages.html" and p.url != "/POD.html" %}
## {{ p.title }}
************
{{ p.content }}
    {% endif %}
  {% endfor %}
{% endfor %}
