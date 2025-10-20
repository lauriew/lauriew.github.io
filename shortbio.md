---
layout: default
title: Short Bio
permalink: /shortbio/
---

## Short Biography
--- 
{% for paragraph in site.data.shortbio.bio %}
{{ paragraph | markdownify }}

{% endfor %}
