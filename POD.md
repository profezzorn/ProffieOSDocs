---
title: Single-page documentation
---

{% assign dirs = site.pages | group_by: "dir" | sort: "name" %} 

{% for dir in dirs %}
# {{ dir | capitalize }}
  {% for page in dir.items %}
## {{ p.title }}
{{ p.content }}
  {% endfor %}
{% endfor %}
