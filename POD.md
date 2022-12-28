---
title: Single-page documentation
---

{% include fix_links_header.html %}

{% assign dirs = site.pages | group_by: "dir" | sort: "name" %} 

{% for dir in dirs %}
{%if dir.name != "/" and dir.name != "/assets/css/" %}
*****
# {{ dir.name | remove_first: "/" | split: "/" | join: ", " | capitalize }}
*****
{% endif %}
  {% for p in dir.items %}
    {% if p.title and p.url != "/" and p.url != "/all_pages.html" and p.url != "/POD.html" %}
<div id="{{ p.id | slugify }}">
## {{ p.title }}
************
{{ p.content }}
</div>
{% include fix_links.html from_url=p.url to_url=p.id %}
<center><img src="/images/pod.svg" width=75 height=120></center>
    {% endif %}
  {% endfor %}
{% endfor %}

{% include fix_links_footer.html %}
