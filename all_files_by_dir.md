---
title: All ProffieOS Documentation Pages
---
Complete index of all pages on this site:

{% assign dirs = site.pages | group_by: "dir" | sort: "name" %} 

{% for dir in dirs %}
## {{ dir | capitalize }}
{% for p in dir.items %}{% if p.title %}
  * [{{ p.title }}]({{ p.url }}){% endif %}{% endfor %}
{% endfor %}
