---
title: Display pages
meta: true
---

{% assign pages = site.pages | where: "dir", page.url | sort: "title" %} 
{% for p in pages %}{% if p.title %}
  * [{{ p.title }}]({{ p.url }}){% endif %}{% endfor %}
