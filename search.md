---
title: Search page
list: false
---
<script>
  var index = elasticlunr(function () {
    this.addField('title');
    this.addField('body');
    this.setRef('id');
});
</script>

{% for p in site.pages %}
  {% if p.title and p.url != "/" and p.url != "/all_pages.html" and p.url != "/POD.html" %}
    <div class=podsearch id="{{ p.url | escape }}" title="{{ p.title | xml_escape }}">
      {{ content })
    </div>
  {% endif %}
{% endfor %}
