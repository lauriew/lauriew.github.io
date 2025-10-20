---
layout: default
title: Publications
permalink: /publications/
---

## Publications
---
<div id="books-list"></div>
<div id="journal-articles-list"></div>
<div id="conference-papers-list"></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bibtex-parse-js@0.0.24/bibtexParse.min.js"></script>

<script>
function loadBib(file, containerId, sectionTitle) {
  fetch(file)
    .then(response => response.text())
    .then(bibtex => {
      const parsed = bibtexParse.toJSON(bibtex);

      // Sort by year descending
      parsed.sort((a, b) => (b.entryTags.year || 0) - (a.entryTags.year || 0));

      let html = `<h2>${sectionTitle}</h2><ol>`;
      parsed.forEach(entry => {
        const tags = entry.entryTags;
        html += '<li style="margin-bottom: 20px;">';

        if (tags.author) html += `<strong>${tags.author}</strong>. `;
        if (tags.title) html += `"${tags.title}." `;
        if (tags.journal) html += `<em>${tags.journal}</em>`;
        else if (tags.booktitle) html += `<em>${tags.booktitle}</em>`;
        if (tags.volume) html += `, vol. ${tags.volume}`;
        if (tags.number) html += `, no. ${tags.number}`;
        if (tags.pages) html += `, pp. ${tags.pages}`;
        if (tags.year) html += `, ${tags.year}.`;

        html += '</li>';
      });
      html += '</ol>';

      document.getElementById(containerId).innerHTML = html;
    })
    .catch(error => {
      document.getElementById(containerId).innerHTML = 
        `<p>Error loading ${sectionTitle}. Check console.</p>`;
      console.error(`Error loading ${file}:`, error);
    });
}

// Load each bibliography file
loadBib('{{ site.baseurl }}/assets/books.bib', 'books-list', 'Books');
loadBib('{{ site.baseurl }}/assets/journal_articles.bib', 'journal-articles-list', 'Journal Articles');
loadBib('{{ site.baseurl }}/assets/conference_publications.bib', 'conference-papers-list', 'Conference Papers');
</script>
