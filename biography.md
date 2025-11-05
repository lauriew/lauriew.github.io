---
layout: default
title: Biography
permalink: /biography/
---

# Biography
--- 
{% for paragraph in site.data.biography.bio %}
{{ paragraph | markdownify }}

{% endfor %}
