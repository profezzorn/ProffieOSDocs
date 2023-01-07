---
title: Howtos
meta: true
---

{% assign pages = site.pages | where: "dir", page.url | sort: "title" %} 
{% for p in pages %}{% if p.title and p.url != dir.name %}
  * [{{ p.title }}]({{ p.url }}){% endif %}{% endfor %}
