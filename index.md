---
layout: default
title: Home
---

<div class="profile-section">
  <div class="profile-content">
    {% for paragraph in site.data.index.profile.description %}
      <p>{{ paragraph | markdownify }}</p>
    {% endfor %}
  </div>
  <div>
    <img src="{{ site.baseurl }}{{ site.data.index.profile.profile_image }}" alt="{{ site.data.home.profile.name }}" class="profile-image">
  </div>
</div>

# Contact Information
---
<p>
<strong>Office:</strong> {{ site.data.index.contact.office }}<br>
<strong>Phone:</strong> {{ site.data.index.contact.phone }}<br>
<strong>Fax:</strong> {{ site.data.index.contact.fax }}<br>
<strong>Email:</strong> {{ site.data.index.contact.email }}
</p>
