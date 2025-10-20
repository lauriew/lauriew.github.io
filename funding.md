---
layout: default
title: Funding
permalink: /funding/
---

## Research Funding
### Below is a summary of funded research projects led or co-led by **Dr. Laurie Williams**. 

{% for grant in site.data.funding.funds %}
---

### **{{ grant.title }}**
**Agency/Program:** {{ grant.agency }}  
**Duration:** {{ grant.duration }}  
**Principal Investigator:** {{ grant.pi }}{% if grant.co_pi %} (Co-PIs: {{ grant.co_pi }}){% endif %}  
**Amount:** {{ grant.amount }}  

{{ grant.description }}

---
{% endfor %}

_Last updated: {{ site.data.funding.last_updated }}_
