---
title: All ProffieOS Documentation Pages
meta: true
---

{% assign dirs = site.pages | group_by: "dir" | sort: "name" %} 

{% for dir in dirs %}
{%if dir.name != "/" and dir.name != "/assets/css/" %}
## {{ dir.name | remove_first: "/" | split: "/" | join: ", " | capitalize }}
{% endif %}
{% for p in dir.items %}{% if p.title %}
  * [{{ p.title }}]({{ p.url }}){% endif %}{% endfor %}
{% endfor %}
