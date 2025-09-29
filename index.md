---
title: Home
layout: default
---

Semantics and Linguistic Theory (SALT) {{ site.saltnum }} will be hosted by the Linguistics Department at the {{ site.uni }} on {{ site.dates }}, {{ site.year }}. The conference will be held solely in-person, and there will be no remote presentation or attendance option.

For questions or comments, please contact <span style="font-family: monospace">[salt36.uba@gmail.com](mailto:salt36.uba@gmail.com)</span>. By attending, you agree to abide by the [Code of Conduct]({{ "/code-of-conduct/" | relative_url }}).


<!--- As part of SALT{{ site.saltnum }}, the SALT Equity and Diversity Committee (SALTED) and the SALT{{ site.saltnum }} organizing committee will hold a workshop: *...*. --->

<hr/>

## Invited speakers

<ul id="speakers">
  {% for presentation in site.data.presentations.keynotes %}
    {% if presentation[0] != "name" %}
      {% assign speakerid = presentation[1].authors[0] %}
      {% assign speaker = site.data.people[speakerid] %}
      <li>
        {% if speaker.website != null %}<a href="{{ speaker.website }}">{{ speaker.name }}</a>{% else %}{{ speaker.name }}{% endif %} ({{ speaker.institutions | join: ", " }})
      </li>
    {% endif %}
  {% endfor %}
</ul>

<hr/>

## Announcements

<table class="announce">
  <tbody>
    {% for announcement in site.data.announcements %}
    <tr>
      <td class="time">
        [{{ announcement.date }}]
      </td>
      <td>
        {{ announcement.text }}
      </td>
    </tr>
    {% endfor %}
  </tbody>
</table>
<!-- <hr style="border-style: dashed; border-color: #eae9e6"> -->

<hr/>

## Important dates

<table class="announce">
  <tbody>
    {% for milestone in site.data.important_dates %}
    <tr>
      <td class="time">
        [{{ milestone.date }}]
      </td>
      <td>
        {{ milestone.text }}
      </td>
    </tr>
    {% endfor %}
  </tbody>
</table>

<hr/>

## Organizing Committee

<ul id="speakers">

    {% for organizer_id in site.data.organizers %}
    {% assign organizer = site.data.people[organizer_id] %}
    <li>
      {% if organizer.website %}
        <a href="{{ organizer.website }}">{{ organizer.name }}</a>
      {% else %}
        {{ organizer.name }}
      {% endif %}
      ({{ organizer.institutions | join: ", " }})
      </li>
  {% endfor %}
</ul>

## Sponsors

SALT{{ site.saltnum }} is sponsored by the [Facultad de Filosofía y Letras](https://filo.uba.ar/) of the [Universidad de Buenos Aires](https://uba.ar/). The [Linguistic Society of America](https://www.lsadc.org/) handles the registration and publishes [the conference proceedings](https://journals.linguisticsociety.org/proceedings/index.php/SALT).
