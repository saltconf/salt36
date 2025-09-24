---
title: Abstracts
layout: default
---

{% for group in site.data.presentations %}
  <h1>{{ group[1].name }}<a id="{{ group[0] }}"></a></h1>
  <ul>
    {% for presentation in group[1] %}
      {% if presentation[1].title != null %}
      <li>
      {% if presentation[1].abstract_formats contains "md" %}
      <a href="{{ site.baseurl }}/abstracts/{{ presentation[0] }}.html">{{ presentation[1].title }}</a>
      {% elsif presentation[1].abstract_formats contains "pdf" %}
        <a href="{{ site.baseurl }}/abstracts/{{ presentation[0] }}.pdf">{{ presentation[1].title }}</a>
      {% else %}
        {{ presentation[1].title }}
      {% endif %}
      {% if presentation[1].materials_format != null %}
        [<a href="{{ site.baseurl }}/presentation-materials/{{ presentation[0] }}.{{ presentation[1].materials_format }}">{% if group[0] == "posters" %}poster{% else %}{{ presentation[1].materials_type }}{% endif %}</a>]
      {% endif %}
      <br/>
      {% for authorid in presentation[1].authors %}
        {% assign author = site.data.people[authorid] %}
        
        {{ author.name }} ({{ author.institutions | join: ", " }})
        {% unless forloop.last %}<br/>{% endunless %}
      {% endfor %}
      </li>
      {% endif %}
    {% endfor %}
  </ul>
{% endfor %}