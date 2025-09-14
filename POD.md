---
title: Single-page documentation
pod: true
meta: true
---

{% assign dirs = site.pages | group_by: "dir" | sort: "name" %} 

{% for dir in dirs %}
{%if dir.name != "/" and dir.name != "/assets/css/" and dir.name != "/r/" %}
*****
# {{ dir.name | remove_first: "/" | split: "/" | join: ", " | capitalize }}
*****
{% endif %}
  {% for p in dir.items %}
    {% if p.title and p.meta != "true" and p.url != "/" and p.url != "/all_pages.html" and p.url != "/POD.html"  and p.url != dir.name and p.url != "/search.html" %}
## {{ p.title }}
************
{{ p.content }}
<center class="pagebreak"><img src="/images/pod.svg" width=75 height=120 class="noprint" ></center>
    {% endif %}
  {% endfor %}
{% endfor %}

