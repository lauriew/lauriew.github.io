---
layout: default
title: Teaching
permalink: /teaching/
---

## Courses
---
<br>

{% for course in site.data.teaching.courses %}
### **{{ course.title }}**
{% if course.resources != "" %}
**Resources:** {{ course.resources }}
{% endif %}
**Overview:** {{ course.overview }}

**Learning Outcomes:**
{% for lo in course.learning_outcomes %}
- {{ lo }}
{% endfor %}
{% endfor %}
