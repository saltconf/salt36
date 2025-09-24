---
title: Program
layout: default
---

<script type="text/javascript">
   function lightning(cls, arr) {
       var rows = document.getElementsByClassName(cls);
       for (var i = 0; i < rows.length; i++) {
	         rows[i].classList.toggle("hidden");
       }
       document.getElementById(arr).classList.toggle("collapsed");
   }
</script>

All talks and posters at SALT{{ site.saltnum }} will take place on the [Bonifacio Annex](https://www.google.com/maps/place/EDIFICIO+ANEXO+FACULTAD+FILOSOF%C3%8DA+(UBA)/@-34.6283188,-58.4461018,21z/) of the FFyL UBA.

<!---Talk sessions and on-site registration will take place on the first floor of ..., and coffee breaks will take place on the first floor of .... On Wednesday evening (May ...), there will be a reception concurrent with the poster session, both in ....--->

<p>
  <!---<b>NB:</b> This schedule is preliminary and subject to change.--->
  <b>Program : TBD</b>
</p>

{% assign lightning_bin = 0 %}
{% assign lightning_bin_str = "One" %}

{% for day in site.data.program %}

<h2 id="{{ day.day }}">{{ day.date }}</h2>

<table class="program">
  <tbody>
    {% for event in day.events %}
    {% if event.type == "talk_session" %}
      {% assign chair = site.data.people[event.chairid] %}
      <tr class="talkChairinfo">
        <td colspan="3">
          {{ event.name }} // chair: <a href="{{ chair.website }}" class="chairName">{{ chair.name }}</a>
        </td>
      </tr>
      {% for talk in event.subevents %}
        {% assign talkinfo = site.data.presentations.talks[talk.talkid] %}
        <tr class="talk">
          <td class="time">{{ talk.time }}</td>
          <td class="title">
            {% if talkinfo.abstract_formats contains "md" %}
              <a href="{{ "/abstracts/" | append: talk.talkid | append: ".html" | relative_url }}">{{ talkinfo.title }}</a>
            {% elsif talkinfo.abstract_formats contains "pdf" %}
              <a href="{{ "/abstracts/" | append: talk.talkid | append: ".pdf" | relative_url }}">{{ talkinfo.title }}</a>
            {% else %}
              {{ talkinfo.title }}
            {% endif %}
            {% if talkinfo.materials_format != null %}
              [<a href="{{ "/presentation-materials/" | append: talk.talkid | append: "." | append: talkinfo.materials_format | relative_url }}">{{ talkinfo.materials_type }}</a>]
            {% endif %}
          </td>
          <td class="authors">
            {% for authorid in talkinfo.authors %}
              {% assign author = site.data.people[authorid] %}
              {% if author.website != null %}
                <a class="authorwebsite" href="{{ author.website }}">{{ author.name }}</a>
              {% else %}
                {{ author.name }}
              {% endif %}
              {% unless forloop.last %}<br/>{% endunless %}
            {% endfor %}
          </td>
        </tr>
      {% endfor %}
    {% elsif event.type == "welcome" %}
    {% assign chair = site.data.people[event.chairid] %}
    <tr>
      <td class="time">{{ event.time }}</td>
      <td class="title" colspan="2">{{ event.name }} by <a href="{{ chair.website }}">{{ chair.name }}</a></td>
    </tr>
    {% elsif event.type == "keynote" %}
    {% assign talkinfo = site.data.presentations.keynotes[event.talkid] %}
    {% assign chair = site.data.people[event.chairid] %}
    <tr class="invitedChairinfo"><td colspan="3">Invited Talk // chair: <a href="{{ chair.website }}" class="chairName">{{ chair.name }}</a></td></tr>
    <tr class="invited">
      <td class="time">{{ event.time }}</td>
      <td class="title">
      {% if talkinfo.abstract_formats contains "md" %}
      <a href="{{ "/abstracts/" | append: event.talkid | append: ".html" | relative_url }}">{{ talkinfo.title }}</a>
      {% elsif talkinfo.abstract_formats contains "pdf" %}
      <a href="{{ "/abstracts/" | append: event.talkid | append: ".pdf" | relative_url }}">{{ talkinfo.title }}</a>
      {% else %}
      {{ talkinfo.title }}
      {% endif %}
      {% if talkinfo.materials_format != null %}
        [<a href="{{ "/presentation-materials/" | append: event.talkid | append: "." | append: talkinfo.materials_format | relative_url }}">{{ talkinfo.materials_type }}</a>]
      {% endif %}
      </td>
      <td class="authors">
        {% for authorid in talkinfo.authors %}
          {% assign author = site.data.people[authorid] %}
          {% if author.website != null %}
          <a class="authorwebsite" href="{{ author.website }}">{{ author.name }}</a>
          {% else %}
          {{ author.name }}
          {% endif %}
          {% unless forloop.last %}<br/>{% endunless %}
        {% endfor %}
      </td>
    </tr>
    {% elsif event.type == "workshop" %}
    {% assign chair = site.data.people[event.chairid] %}
    <tr class="posterChairinfo"><td colspan="3">SALTED Workshop // chair: <a href="{{ chair.website }}" class="chairName">{{ chair.name }}</a></td></tr>
    <tr class="poster">
      <td class="time">{{ event.time }}</td>
      <td class="title" colspan="2"><a href="{{ "/salted/" | relative_url }}">{{ event.name }}</a></td>
    </tr>
    {% elsif event.type == "lightning" %}
    {% assign chair = site.data.people[event.chairid] %}
    <tr class="posterChairinfo"><td colspan="3">Lightning Talk Session // chair: <a href="{{ chair.website }}" class="chairName">{{ chair.name }}</a></td></tr>
    <tr class="postertalk">
      <td class="time">{{ event.time }}</td>
      <td class="title" colspan="2">
        <span id="light{{ lightning_bin_str }}PosterArr" class="collapsed"></span>
        <a id="light{{ lightning_bin_str }}PosterSwitch" href="javascript:void(0)" onclick="lightning('posterInfoLight{{ lightning_bin_str }}', 'light{{ lightning_bin_str }}PosterArr')">{{ event.name }}</a>
      </td>
    </tr>
    {% for posterinfo in site.data.presentations.posters %}
      {% if lightning_bin == posterinfo[1].lightning_bin %}
      <tr class="posterInfoLight{{ lightning_bin_str }} hidden">
        <td class="time">&nbsp;</td>
        <td class="title">
        {% if posterinfo[1].abstract_formats contains "md" %}
        <a href="{{ "/abstracts/" | append: posterinfo[0] | append: ".html" | relative_url }}">{{ posterinfo[1].title }}</a>
        {% elsif posterinfo[1].abstract_formats contains "pdf" %}
        <a href="{{ "/abstracts/" | append: posterinfo[0] | append: ".pdf" | relative_url }}">{{ posterinfo[1].title }}</a>
        {% else %}
        {{ posterinfo[1].title }}
        {% endif %}
        {% if posterinfo[1].materials_format != null %}
          [<a href="{{ "/presentation-materials/" | append: posterinfo[0] | append: "." | append: posterinfo[1].materials_format | relative_url }}">poster</a>]
        {% endif %}
        </td>
        <td class="authors">
        {% for authorid in posterinfo[1].authors %}
          {% assign author = site.data.people[authorid] %}
          {% if author.website != null %}
          <a class="authorwebsite" href="{{ author.website }}">{{ author.name }}</a>
          {% else %}
          {{ author.name }}
          {% endif %}
          {% unless forloop.last %}<br/>{% endunless %}
        {% endfor %}
        </td>
      </tr>
      {% endif %}
    {% endfor %}
    {% assign lightning_bin = 1 %}
    {% assign lightning_bin_str = "Two" %}
    {% elsif event.type == "poster" %}
    <tr class="posterChairinfo"><td colspan="3">Poster Session</td></tr>
    <tr class="postertalk">
      <td class="time">{{ event.time }}</td>
      <td class="title" colspan="2">{{ event.name }}</td>
    </tr>
    {% else %}
    <tr class="{{ event.type }}">
      <td class="time">{{ event.time }}</td>
      <td class="title" colspan="2">{{ event.name }}</td>
      <td></td>
    </tr>
    {% endif %}
    {% endfor %}
  </tbody>
</table>

{% endfor %}
