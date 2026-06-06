---
title: Program
layout: default
---

All talks and posters at SALT{{ site.saltnum }} will take place on the [Bonifacio Annex](https://www.google.com/maps/place/EDIFICIO+ANEXO+FACULTAD+FILOSOF%C3%8DA+(UBA)/@-34.6283188,-58.4461018,21z/) of the FFyL UBA.

<!---Talk sessions and on-site registration will take place on the first floor of ..., and coffee breaks will take place on the first floor of .... On Wednesday evening (May ...), there will be a reception concurrent with the poster session, both in ....--->

<p>
<b>NB:</b> This schedule is preliminary and subject to change.
</p>

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
            {% if talkinfo.abstract_formats contains "http" %}
              <a href="{{ talkinfo.abstract_formats }}">{{ talkinfo.title }}</a>      
            {% elsif talkinfo.abstract_formats contains "md" %}
              <a href="/salt36/abstracts/{{ event.talkid }}.md">{{ talkinfo.title }}</a>
            {% elsif talkinfo.abstract_formats contains "pdf" %}
              <a href="/salt36/abstracts/{{ event.talkid }}.pdf">{{ talkinfo.title }}</a>
            {% else %}
              {{ talkinfo.title }}
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
    {% elsif event.type == "poster" %}
      <tr class="posterChairinfo">
        <td colspan="3">Poster Session {{ event.session }}</td>
      </tr>
      {% assign first_poster = true %}
      {% for posterinfo in site.data.presentations.posters %}
        {% if posterinfo[1].poster_session == event.session %}
          <tr class="posterInfo">
            {% if first_poster %}
              <td class="time posterTime">{{ event.time }}</td>
              {% assign first_poster = false %}
            {% else %}
              <td class="time posterTime posterTimeContinued"></td>
            {% endif %}
            <td class="title">
              {% if posterinfo[1].abstract_formats contains "http" %}
                <a href="{{ posterinfo[1].abstract_formats }}">{{ posterinfo[1].title }}</a>
              {% else %}
                {{ posterinfo[1].title }}
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
