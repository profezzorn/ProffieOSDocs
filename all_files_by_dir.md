---
title: All ProffieOS Documentation Pages
---
Complete index of all pages on this site:

{% assign dirs = site.pages | group_by: "dir" | sort: "name" %} 

{% for dir in dirs %}
{%if dir.name != "/" and dir.name != "/assets/css/" %}
{% assign header = dir.name | remove_first: "/" | split: "/" | join: ", " | capitalize %}
## {{ dir.name| capitalize }}
{% for p in dir.items %}{% if p.title %}
  * [{{ p.title }}]({{ p.url }}){% endif %}{% endfor %}
{% endif %}
{% endfor %}
