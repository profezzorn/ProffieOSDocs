---
title: All ProffieOS Documentation Pages
---
Complete index of all pages on this site:

{% for p in site.pages %}{% if p.title %}
  * [{{ p.title }}]({{ p.url }}){% endif %}{% endfor %}


<!-- testing...

  {% assign dirs = site.pages | group_by: "dir" %} 

  dirs = {{ dirs }}

  {% for dir in dirs %}
     {% for page in dir.items %}
          {{ dir.name }} / {{ page.url }} : {{ page.title }}
     {% endfor %}
  {% endfor %}
-->
