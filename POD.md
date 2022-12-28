---
title: Single-page documentation
pod: true
---

{% assign dirs = site.pages | group_by: "dir" | sort: "name" %} 

{% for dir in dirs %}
{%if dir.name != "/" and dir.name != "/assets/css/" %}
*****
# {{ dir.name | remove_first: "/" | split: "/" | join: ", " | capitalize }}
*****
{% endif %}
  {% for p in dir.items %}
    {% if p.title and p.url != "/" and p.url != "/all_pages.html" and p.url != "/POD.html" %}
<div id="PAGE-{{p.title | slugify }}"></div>
## {{ p.title }}
************
{{ p.content }}
<center><img src="/images/pod.svg" width=75 height=120></center>
    {% endif %}
  {% endfor %}
{% endfor %}

