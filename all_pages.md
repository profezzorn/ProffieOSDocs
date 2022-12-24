
Complete index of all pages on this site:


{% for p in site.pages | sort %}{% if p.url contains ".html" %}
  * [{% if p.title %}{{ p.title }}{% else %}{{p.url | replace_first: "/", " " | replace: "/", ", " | replace: "-", " " | remove: ".html" }}{% endif %}]({{ p.url}})
{% endif %} {% endfor %}
