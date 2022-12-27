---
title: All ProffieOS Documentation Pages
---
Complete index of all pages on this site:

{% for p in site.pages %}{% if p.title %}
  * [{{ p.title }}]({{ p.url }}){% endif %}{% endfor %}


<!-- testing...

  {% assign dirs = "" | split: "x" %}
  {% for page in site.pages %}
     {% if dirs contains page.dir %}
     {% else %}
       {% assign tmp = pages.dir | split: ":" %}
       {% assign dirs = pages | concat: tmp %}
     {% endif %}
  {% endfor %}
  {% assign dirs = dirs | sort %}

dirs = {{ dirs }}

  {% for dir in dirs %}
     {% for page in pages %}
       {% if page.dir == dir %}
          {{ page.dir }} / {{ page.url }} : {{ page.title }}
       {% endif %}
     {% endfor %}
   {% endfor %}
-->
