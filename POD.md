---
title: Single-page documentation
---

{% raw %}
<script>
  var linksToFix = {};
  function fixPODLink(f, t) {
    linksToFix[f] = t;
    linksToFix[new URL(f, window.location).href] = t;
  }
</script>
{% endraw %}

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
{% raw %}
  <script>fixPODLink("{{ p.url | escape }}", "#{{ p.id | slugify }}");</script>
{% endraw %}
<center><img src="/images/pod.svg" width=75 height=120></center>
    {% endif %}
  {% endfor %}
{% endfor %}

{% raw %}
<script>
  document.getElementsByTag("a").forEach(function(tag) {
     var href = tag.href;
     if (linksToFix[href]) {
       tag.href = linksToFix[href];
     } else {
       var href2 = new URL(href, window.location).href;
       if (linksToFix[href2]) {
         tag.href = linksToFix[href2];
         linksToFix[href] = linksToFix[href2];
       }
     }
  });
</script>
{% endraw %}
