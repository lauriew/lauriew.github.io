---
layout: default
title: Students
permalink: /students/
---

## Current Post Docs

<ul>
{% for doc in site.data.students.current_post_docs %}
  <li>
    <strong>{{ doc.name }}</strong>
    {% if doc.linkedin or doc.portfolio %}
      <br>
      {% if doc.linkedin %}
        <a href="{{ doc.linkedin }}" target="_blank">LinkedIn</a>
      {% endif %}
      {% if doc.portfolio %}
        {% if doc.linkedin %} | {% endif %}
        <a href="{{ doc.portfolio }}" target="_blank">Portfolio</a>
      {% endif %}
    {% endif %}
  </li>
{% endfor %}
</ul>

---

## Current Students

<ul>
{% for student in site.data.students.current_students %}
  <li>
    <strong>{{ student.name }}</strong>
    {% if student.degree %} ({{ student.degree }}){% endif %}
    {% if student.linkedin or student.portfolio %}
      <br>
      {% if student.linkedin %}
        <a href="{{ student.linkedin }}" target="_blank">LinkedIn</a>
      {% endif %}
      {% if student.portfolio %}
        {% if student.linkedin %} | {% endif %}
        <a href="{{ student.portfolio }}" target="_blank">Portfolio</a>
      {% endif %}
    {% endif %}
  </li>
{% endfor %}
</ul>

---

## Past Post Docs

<ul>
{% for doc in site.data.students.past_post_docs %}
  <li>
    <strong>{{ doc.name }}</strong>
    {% if doc.affiliation %} — {{ doc.affiliation }}{% endif %}
    {% if doc.linkedin or doc.portfolio %}
      <br>
      {% if doc.linkedin %}
        <a href="{{ doc.linkedin }}" target="_blank">LinkedIn</a>
      {% endif %}
      {% if doc.portfolio %}
        {% if doc.linkedin %} | {% endif %}
        <a href="{{ doc.portfolio }}" target="_blank">Portfolio</a>
      {% endif %}
    {% endif %}
  </li>
{% endfor %}
</ul>

---

## Graduated PhD Students

<ul>
{% for phd in site.data.students.graduated_phd %}
  <li>
    <strong>{{ phd.name }}</strong>
    {% if phd.year %} ({{ phd.year }}){% endif %}
    {% if phd.employer %}, {{ phd.employer }}{% endif %}
    <br>
    <em>Dissertation:</em> {{ phd.dissertation }}
    {% if phd.notes %}<br><em>{{ phd.notes }}</em>{% endif %}
    {% if phd.linkedin or phd.portfolio or phd.thesis_link %}
      <br>
      {% if phd.linkedin %}
        <a href="{{ phd.linkedin }}" target="_blank">LinkedIn</a>
      {% endif %}
      {% if phd.portfolio %}
        {% if phd.linkedin %} | {% endif %}
        <a href="{{ phd.portfolio }}" target="_blank">Portfolio</a>
      {% endif %}
      {% if phd.thesis_link %}
        {% if phd.linkedin or phd.portfolio %} | {% endif %}
        <a href="{{ phd.thesis_link }}" target="_blank">Dissertation</a>
      {% endif %}
    {% endif %}
  </li>
{% endfor %}
</ul>

---

## Graduated MS Students

<ul>
{% for ms in site.data.students.graduated_ms %}
  <li>
    <strong>{{ ms.name }}</strong>
    {% if ms.year %} ({{ ms.year }}){% endif %}
    {% if ms.employer %}, {{ ms.employer }}{% endif %}
    <br>
    <em>Thesis:</em> {{ ms.thesis }}
    {% if ms.linkedin or ms.portfolio or ms.thesis_link %}
      <br>
      {% if ms.linkedin %}
        <a href="{{ ms.linkedin }}" target="_blank">LinkedIn</a>
      {% endif %}
      {% if ms.portfolio %}
        {% if ms.linkedin %} | {% endif %}
        <a href="{{ ms.portfolio }}" target="_blank">Portfolio</a>
      {% endif %}
      {% if ms.thesis_link %}
        {% if ms.linkedin or ms.portfolio %} | {% endif %}
        <a href="{{ ms.thesis_link }}" target="_blank">Thesis</a>
      {% endif %}
    {% endif %}
  </li>
{% endfor %}
</ul>

---