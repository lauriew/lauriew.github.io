---
layout: default
title: Publications
permalink: /publications/
---

## Publications

<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bibtex-parse-js@0.0.24/bibtexParse.min.js"></script>

<div id="publications-list"></div>

<script>
fetch('{{ site.baseurl }}/assets/references.bib')
  .then(response => response.text())
  .then(bibtex => {
    const parsed = bibtexParse.toJSON(bibtex);
    let html = '<ol>';
    
    // Sort by year descending
    parsed.sort((a, b) => (b.entryTags.year || 0) - (a.entryTags.year || 0));
    
    parsed.forEach(entry => {
      const tags = entry.entryTags;
      html += '<li style="margin-bottom: 20px;">';
      
      // Authors
      if (tags.author) {
        html += `<strong>${tags.author}</strong>. `;
      }
      
      // Title
      if (tags.title) {
        html += `"${tags.title}." `;
      }
      
      // Journal or Booktitle
      if (tags.journal) {
        html += `<em>${tags.journal}</em>`;
      } else if (tags.booktitle) {
        html += `<em>${tags.booktitle}</em>`;
      }
      
      // Volume and pages
      if (tags.volume) {
        html += `, vol. ${tags.volume}`;
      }
      if (tags.number) {
        html += `, no. ${tags.number}`;
      }
      if (tags.pages) {
        html += `, pp. ${tags.pages}`;
      }
      
      // Year
      if (tags.year) {
        html += `, ${tags.year}.`;
      }
      
      html += '</li>';
    });
    
    html += '</ol>';
    document.getElementById('publications-list').innerHTML = html;
  })
  .catch(error => {
    document.getElementById('publications-list').innerHTML = 
      '<p>Error loading publications. Please check the console.</p>';
    console.error('Error:', error);
  });
</script>