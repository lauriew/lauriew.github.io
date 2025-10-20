---
layout: default
title: Students
permalink: /students/
---

## Guidelines for Current and Prospective Students

- [PhD Students Guidelines](/guidelines/phd/)
- [MS Students Guidelines](/guidelines/ms/)

---

## Current Post Docs

<ul>
{% for doc in site.data.students.current_post_docs %}
  <li>
    {% if doc.portfolio or doc.linkedin %}
      <strong><a href="{{ doc.portfolio | default: doc.linkedin }}" target="_blank">{{ doc.name }}</a></strong>
    {% else %}
      <strong>{{ doc.name }}</strong>
    {% endif %}
    {% if doc.linkedin and doc.portfolio %}
      <br>
      <a href="{{ doc.linkedin }}" target="_blank">LinkedIn</a> | <a href="{{ doc.portfolio }}" target="_blank">Portfolio</a>
    {% endif %}
  </li>
{% endfor %}
</ul>

---

## Current Students

<ul>
{% for student in site.data.students.current_students %}
  <li>
    {% if student.portfolio or student.linkedin %}
      <strong><a href="{{ student.portfolio | default: student.linkedin }}" target="_blank">{{ student.name }}</a></strong>
    {% else %}
      <strong>{{ student.name }}</strong>
    {% endif %}
    {% if student.degree %} ({{ student.degree }}){% endif %}
    {% if student.linkedin and student.portfolio %}
      <br>
      <a href="{{ student.linkedin }}" target="_blank">LinkedIn</a> | <a href="{{ student.portfolio }}" target="_blank">Portfolio</a>
    {% endif %}
  </li>
{% endfor %}
</ul>

---

## Past Post Docs

<ul>
{% for doc in site.data.students.past_post_docs %}
  <li>
    {% if doc.portfolio or doc.linkedin %}
      <strong><a href="{{ doc.portfolio | default: doc.linkedin }}" target="_blank">{{ doc.name }}</a></strong>
    {% else %}
      <strong>{{ doc.name }}</strong>
    {% endif %}
    {% if doc.affiliation %} — {{ doc.affiliation }}{% endif %}
    {% if doc.linkedin and doc.portfolio %}
      <br>
      <a href="{{ doc.linkedin }}" target="_blank">LinkedIn</a> | <a href="{{ doc.portfolio }}" target="_blank">Portfolio</a>
    {% endif %}
  </li>
{% endfor %}
</ul>

---

## Graduated PhD Students

<ul>
{% for phd in site.data.students.graduated_phd %}
  <li>
    {% if phd.portfolio or phd.linkedin %}
      <strong><a href="{{ phd.portfolio | default: phd.linkedin }}" target="_blank">{{ phd.name }}</a></strong>
    {% else %}
      <strong>{{ phd.name }}</strong>
    {% endif %}
    {% if phd.year %} ({{ phd.year }}){% endif %}
    {% if phd.employer %}, {{ phd.employer }}{% endif %}
    <br>
    <em>Dissertation:</em> 
    {% if phd.thesis_link %}
      <a href="{{ phd.thesis_link }}" target="_blank">{{ phd.dissertation }}</a>
    {% else %}
      {{ phd.dissertation }}
    {% endif %}
    {% if phd.notes %}<br><em>{{ phd.notes }}</em>{% endif %}
    
  </li>
{% endfor %}
</ul>

---

## Graduated MS Students

<ul>
{% for ms in site.data.students.graduated_ms %}
  <li>
    {% if ms.portfolio or ms.linkedin %}
      <strong><a href="{{ ms.portfolio | default: ms.linkedin }}" target="_blank">{{ ms.name }}</a></strong>
    {% else %}
      <strong>{{ ms.name }}</strong>
    {% endif %}
    {% if ms.year %} ({{ ms.year }}){% endif %}
    {% if ms.employer %}, {{ ms.employer }}{% endif %}
    <br>
    <em>Thesis:</em> 
    {% if ms.thesis_link %}
      <a href="{{ ms.thesis_link }}" target="_blank">{{ ms.thesis }}</a>
    {% else %}
      {{ ms.thesis }}
    {% endif %}
  </li>
{% endfor %}
</ul>

---