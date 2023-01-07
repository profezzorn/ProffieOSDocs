---
title: Configuration
meta: true
---

{% assign pages = site.pages | where: "dir", page.url | sort: "title" %} 
{% for p in pages %}{% if p.title and p.url != page.url %}
  * [{{ p.title }}]({{ p.url }}){% endif %}{% endfor %}
